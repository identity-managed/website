---
draft: false
title: SQL Always On Availability Groups for MIM
description: SQL Always On Availability Groups for MIM
tags:
  - SQL
  - Clustering
  - AOA
  - Microsoft Identity Manager
  - LogShipping
  - High Availability
  - MIM
  - SQL Clustering
  - Mirroring
categories:
  - MIM
date: 2022-04-26T14:31:00.004-07:00
authors:
  - David
url: /2022/04/sql-always-on-availability-groups-for.html
---

Edited July 2 2022 after reviewing my Facebook discussion with Eugene Sergeev on Microsoft's product team.

MIM 2016 SP2 (and 4.4.1459.0 or later [supports SQL Server Always On Availability Groups](https://support.microsoft.com/en-us/help/3200896/sql-server-availability-solutions-for-microsoft-identity-manager-servi) (AG))! Yeah!

Ok let's implement it!

  

**But wait!** It won't give us all we hope for!

  

*   Up to the moment distributed backup of the data -- yes!
*   Automatic instant failover -- not without a huge caveat!

What do you mean it won't give us Automatic Instant Failover?

  

Let's discuss what AG's give us over the old SQL Failover cluster and mirroring

  

**Failover Clustering**

  

With SQL Server (prior to SQL Server 2012) Failover clustering we have two or more servers in the same subnet (they can be in different datacenters via a stretch VLAN). When the active node goes offline then one of the other nodes will try to grab the necessary resources for that service, and bring them online. One of the critical pieces to note is that the Service has a virtual server name and virtual IP address. DNS points the virtual server name at the virtual IP address. During a failover, the new active node [grabs the virtual IP address and sends out a gratuitous ARP request](https://support.microsoft.com/en-us/help/244331/mac-address-changes-for-virtual-server-during-a-failover-with-clusteri), which causes all devices on the subnet (including the router) to update the MAC address associated with the Virtual IP Address. So almost instantly requests for that IP address will be sent to the newly active node.

  

**Failover Clustering on Multiple Subnets**

Starting with SQL Server 2012 we gained the ability to do [failover clustering](http://sqlsoldier.net/wp/sqlserver/multsubnetfailoverclusters)  over multiple subnets. However, failover is much slower as we would now depend on the cluster updating DNS, and DNS needs to replicate as well as DNS records have a time to live (TTL) which tells clients how long to cache the DNS record. The default TTL for cluster registered DNS records in 20 minutes. Which means that it could take 20 mins plus DNS replication time (default is every 180 minutes) for all clients to find the new server. Of course you can lower this, but I wouldn't go below 60 seconds. If your DNS doesn't or isn’t taking dynamic registrations from your SQL Server then you have to update it by hand.

  

**SQL Mirroring**

With [SQL Mirroring](https://docs.microsoft.com/en-us/sql/database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server?view=sql-server-ver15) we have two or more servers in the same subnet or different subnets, where one server is principal for a database and the others are mirroring/receiving the transactions either synchronously or asynchronously. Synchronous mirroring with a witness provides for instant failover to a database server in a remote subnet, provided that the client could support the failover\_partner parameter in a connection string, or the application would allow you to do that. Of course, if the server specified in the connection string as the data source is up the server can pass the client the name of the failover partner. But it didn't provide for other databases to failover with it as a unit. It also meant that you needed to manage the connection strings, not such a daunting task for only a few clients. 

  

**Always On Availability Groups**

SQL 2012 also brought Always On Availability Groups or AGs. With an AG you can group databases together and have them fail over as a unit. You create a listener (a Virtual Server Name and set of IP addresses). The cluster registers the Name with DNS and depending on the cluster parameter [RegisterAllProvidersIP](https://www.sqlservercentral.com/blogs/change-registerallprovidersip-setting-on-an-existing-availability-group) it will register all of the IP addresses for all of the nodes hosting the availability group. If in your connection string you set [MultiSubNetFailover](https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server?view=sql-server-ver15#FollowUp)\=TRUE, if your provider supports it, then your client will simultaneously try all of the IP addresses listed and then whichever one responds first (the one hosting the primary replica) will be used. Otherwise, if the MultiSubNetFailover=FALSE or your provider doesn't support it, but RegisterAllProvidersIP =1 on the cluster the client will [try all of the IP address returned from DNS, serially, rather than in parallel,](https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server?view=sql-server-ver15) which could result in substantial delays connecting to the server. 

  

**What does this mean for MIM?**

Now we can turn out attention back to MIM. [MIM uses the SQL Native Client 11.0 OLEDB](https://support.microsoft.com/en-us/help/3200896/sql-server-availability-solutions-for-microsoft-identity-manager-servi) which doesn't support the MultiSubNetFailover keyword. [Additional Info on timeouts](https://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/). In fact, this provider was deprecated until March 2018 . When they released [version 18 which adds support for the MultiSubnetFailover keyword](https://docs.microsoft.com/en-us/sql/connect/oledb/release-notes-for-oledb-driver-for-sql-server?view=sql-server-ver15).  

Per Eugene Sergeev, you could put a second NIC into the MIM server and put it on the other subnet where the other SQL Server is and then you get failover in about 10 seconds. This bypasses the DNS issues.

  

**Does MIM use this new provider?** 

Maybe! No mention of it in [SP2 release notes](https://support.microsoft.com/en-us/help/4512924/microsoft-identity-manager-2016-service-pack-2-build-4-6-34-0-update-r)  but in the [hotfix prior to MIM 2016 SP2, 4.5.412.0, the article](https://support.microsoft.com/en-us/help/4489646/hotfix-rollup-4-5-412-0-available-for-mim-2016-sp1) references this [new ole db provider](https://docs.microsoft.com/en-us/sql/connect/oledb/release-notes-for-oledb-driver-for-sql-server?view=sql-server-ver15): 

*   TLS 1.2 support is added to the MIM Service and Portal installer. This update will install if TLS 1.2 is the only enabled protocol .  
*   After you install this update, the change-mode setup of the MIM Service and Portal will succeed by having only TLS 1.2 enabled and SQL OLE DB driver installed.  
*   **Microsoft OLE DB Driver 18 for SQL Server must be installed**:

But this only references the MIM Service and Portal and not the sync engine. Furthermore, the connection string would still have to change to MultiSubnetFailover=TRUE.

  

Even if it didn't, we could still cheat if we could [control the connection string](https://docs.microsoft.com/en-us/sql/database-engine/listeners-client-connectivity-application-failover?view=sql-server-2014): "If an availability group possesses only one secondary replica and is not configured to allow read-access to the secondary replica, clients can connect to the primary replica by using a database mirroring connection string." But MIM builds the connection string from the parameters in the registry. It does not allow us to control the connection string to the sync engine DB or the FIM Service DB.

  

Per Eugene: "MIM Sync is running under .net v4 runtime, even though compiled for 3.5. However, DB access code is c++ and it indeed uses that old driver that does not support multisubnetfailover=true keyword"

  

So [MIM supports High Availability Groups for SQL](https://support.microsoft.com/en-us/help/3200896/sql-server-availability-solutions-for-microsoft-identity-manager-servi)  but "Synchronization server HA is not supported." 

We are also told that "The SQLNCLI OLE DB Provider does not support the MultiSubnetFailover keyword. To use the MultiSubnetFailover keyword, use the ODBC driver." 

  

Hmm, could we switch all of the services to use the ODBC provider? NO! Not that I have found. The documentation doesn't provide a way to do that. Therefore, this can only refer to SQL connections made using an MA.

  

Per Eugene: "As for ODBC drivers - ignore that part. Only GSQL MA uses ODBC."

  

**So what does the "support" for High Availability Groups give us?** 

We get distributed mirroring that can automatically failover, albeit very slowly subject to DNS TTL. In the meantime the services will have failed. 

*   The FIM Service will retry 10 times with a 6 second timeout after which it fails. 
*   The FIM Synchronization service timeout and retries isn't specified. 

*   But it too will fail, especially if in the middle of a sync. 

*   So we can configure the Services to restart after a short delay. 
*   So if we lower the HostRecordTTL cluster parameter to 60 seconds and configure services to restart we might have an automatic failover.

If you set the RegisterAllProvidersIP to 1 then you will get timeouts trying to start the sync service and the FIM service some of the time. If it set to 0 then you will get timeouts after a failover.

  

This is why the [MIM Prepare SQL guide](https://docs.microsoft.com/en-us/microsoft-identity-manager/prepare-server-sql2016) says: 

MIM 2016 SP2 supports SQL AlwaysOn Availability Group (AoAG) listeners with RegisterAllProvidersIP option set to 0, meaning that SQL Server AoAG cross-subnet failover is not currently supported.

  

So, if you need the MIM Sync database to be highly available you could do an Always on Availability group that is on the same Subnet. If you need it to be distributed you could do a stretch VLAN.

  

Eugene says my summary here is mostly correct: "The bigger deal is the MIM Service, wherein the failure of a SQL connection can lead to workflow failure. Since the code doesn't retry SQL transactions, quicker failover doesn't help us prevent workflow failure"

  

**Bottom line**

The Always on Availability Groups give us a lot of headache and in return we get slightly improved mirroring while the SQL transactions replication/mirroring slows things down. So don't use this if Sync performance or Portal performance is important. Use an AG for MIM PAM or if you have a smaller environment and are doing Password Sync.

  

Otherwise, doing a staging server or a standby server with SQL Log Shipping.

  

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices