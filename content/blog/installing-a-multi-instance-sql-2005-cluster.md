---
title: 'Installing a Multi-Instance SQL 2005 Cluster'
date: 2008-10-15T00:54:00.001-07:00
draft: false
url: /2008/10/installing-multi-instance-sql-2005.html
tags: 
- SQL Clustering
- SQL Server
---

Some of you may run into a problem when installing a multi-instance SQL Server Cluster, in particular when you install the second or third instance in your cluster.

Like this one:

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/InstallingaMultiInstanceSQL2005Cluster_12B3D/image_thumb.png)](http://www.ilmbestpractices.com/blog/uploaded_images/InstallingaMultiInstanceSQL2005Cluster_12B3D/image.png)

Microsoft SQI Server 2005 Setup  
SQL server Setup has determined that the Following account properties are not specified:   
‘SQLBROWSERACCOUNT’. The properties specify the startup account for the services that are installed. To proceed, refer to the template.ini and set the properties to valid account names. If you are specifying a windows user account, you must also specify the password for the account.

This may happen if you install the second instance (virtual server) on a node that is part of the first instance (virtual server). This occurs because the browser service is running on that node.  So SQL setup detects the existence of the browser service and does not prompt you for the credentials for all three services, only for SQL Server and SQL Agent leaving out the SQL Browser. You will then see the above error.

Normally during the install you have the ability to customize all three services:

[![clip_image002](http://www.ilmbestpractices.com/blog/uploaded_images/InstallingaMultiInstanceSQL2005Cluster_12B3D/clip_image002_thumb.jpg)](http://www.ilmbestpractices.com/blog/uploaded_images/InstallingaMultiInstanceSQL2005Cluster_12B3D/clip_image002.jpg)

But when installing the second instance in the cluster on a node that is part of the first virtual server (instance) all you get is this:

[![clip_image002[5]](http://www.ilmbestpractices.com/blog/uploaded_images/InstallingaMultiInstanceSQL2005Cluster_12B3D/clip_image0025_thumb.jpg)](http://www.ilmbestpractices.com/blog/uploaded_images/InstallingaMultiInstanceSQL2005Cluster_12B3D/clip_image0025.jpg)

If you use the same account for all of the services you may not see this error. If you use the same accounts across instances you may not see this error.

That is one other thing that sets this multi-instance SQL cluster apart from others; we tried to follow best practices for security by using separate accounts for each service for each instance. See the two tables below showing the user accounts and global groups created in Active Directory (domain local groups would work too). All of these user and group objects should exist in the same domain as the computer accounts for the Nodes.

### SQL Instance 1

**Parameter**

**Value (filled in by Client)**

Service account for SQL Server Database Engine

DOMAIN\\ MOSS\_SQL\_SER\_1

Group for Service Account for SQL Server Database

DOMAIN\\GMOSS\_SQL\_SER\_1

Members of Group Above

DOMAIN\\ MOSS\_SQL\_SER\_1

Service account for SQL Server Agent

DOMAIN\\ MOSS\_SQL\_AGE\_1

Group for SQL Server Agent

DOMAIN\\ GMOSS\_SQL\_AGE\_1

Members of Group Above

DOMAIN\\ MOSS\_SQL\_AGE\_1

Service account for SQL Server Full Text Engine (FTE)

DOMAIN\\ MOSS\_SQL\_FTE\_1

Group Service account for SQL Server Full Text Engine (FTE)

DOMAIN\\ GMOSS\_SQL\_FTE\_1

Members of Group Above

DOMAIN\\ MOSS\_SQL\_FTE\_1

DOMAIN\\ MOSS\_SQL\_SER\_1

### SQL Instance 2

**Parameter**

**Value (filled in by Client)**

Service account for SQL Server Database Engine

DOMAIN\\ MOSS\_SQL\_SER\_2

Group for Service Account for SQL Server Database

DOMAIN\\GMOSS\_SQL\_SER\_2

Members of Group Above

DOMAIN\\ MOSS\_SQL\_SER\_2

Service account for SQL Server Agent

DOMAIN\\ MOSS\_SQL\_AGE\_2

Group for SQL Server Agent

DOMAIN\\ GMOSS\_SQL\_AGE\_2

Members of Group Above

DOMAIN\\ MOSS\_SQL\_AGE\_2

Service account for SQL Server Full Text Engine (FTE)

DOMAIN\\ MOSS\_SQL\_FTE\_2

Group Service account for SQL Server Full Text Engine (FTE)

DOMAIN\\ GMOSS\_SQL\_FTE\_2

Members of Group Above

DOMAIN\\ MOSS\_SQL\_FTE\_2

DOMAIN\\ MOSS\_SQL\_SER\_2

According to Microsoft CSS (or PSS or whatever you want to call the boys and girls on the other end of the 800 number) the SQL Server Product group is aware of this and has declared that this is an "Expected Program Behavior" (notice the absence of the words bug and feature) that just isn't documented, yet and won't be changed in the future.

However, CSS was kind enough to discuss the workarounds, and help us through them.

There are two workarounds: the first is to install SQL from the command line. You can try to use the command line options or configure an ini file.

Start /wait <CD or DVD Drive>\\servers\\setup.exe /qn

VS=MOSS-ENT-SQL2

INSTALLVS=SQL\_Engine INSTANCENAME=MOSSENTSQL2 ADDLOCAL=SQL\_Engine,Client\_Components ADDNODE=node1,node2,node3

GROUP=MOSS-ENT-SQL2

IP=15.13.15.16,Public 15.13.15.x Interface" ADMINPASSWORD=<StrongPassword>

SAPWD=<StrongPassord>

INSTALLSQLDIR="d:\\Program Files\\Microsoft SQL Server\\" INSTALLSQLDATADIR=”k:\\Microsoft SQL Server” SQLACCOUNT=theDomain\\moss\_sql\_ser\_2 SQLPASSWORD=<DomainUserPassword> AGTACCOUNT=theDomain\\moss\_sql\_age\_2 AGTPASSWORD=<DomainUserPassword> SQLBROWSERACCOUNT=theDomain\\moss\_sql\_ser\_2  SQLBROWSERPASSWORD=<DomainUserPassword> SQLCLUSTERGROUP="theDomain\\gmoss\_sql\_ser\_2" AGTCLUSTERGROUP="theDomain\\gmoss\_sql\_age\_2" FTSCLUSTERGROUP="theDomain\\gmoss\_sql\_ser\_2" ERRORREPORTING=1, SQMREPORTING=1 SQLCOLLATION=SQL\_Latin1\_General\_CP1\_CI\_AS

The pure command line options approach did not work for me and Ramana Akula (Satyam Computer Services), the DBA at the client. If you can find the error in the use of the command line options please let me know.

We did not attempt the ini file method -- perhaps that would have worked.

Since this was a new cluster we took the second workaround: remove one node from the virtual server (SQL instance), which removes the SQL Browser Service, and then run the install on that node. This worked.

To remove a node from an instance or virtual server

1) logon to the node that owns the SQL Instance from which you wish to remove a node.

2) Go to Control Panel -> Add/Remove Programs -> Microsoft SQL Server and click change.

3) Select the instance and click next (ok we cheated on this screen shot this one is actually after we have done everything successfully):

[![clip_image002[7]](http://www.ilmbestpractices.com/blog/uploaded_images/InstallingaMultiInstanceSQL2005Cluster_12B3D/clip_image0027_thumb.jpg)](http://www.ilmbestpractices.com/blog/uploaded_images/InstallingaMultiInstanceSQL2005Cluster_12B3D/clip_image0027.jpg)

4) Then select Database Engine (Clustered) and click Next

[![clip_image002[9]](http://www.ilmbestpractices.com/blog/uploaded_images/InstallingaMultiInstanceSQL2005Cluster_12B3D/clip_image0029_thumb.jpg)](http://www.ilmbestpractices.com/blog/uploaded_images/InstallingaMultiInstanceSQL2005Cluster_12B3D/clip_image0029.jpg)

5) Then click Next on the Welcome Wizard.

[![clip_image002[11]](http://www.ilmbestpractices.com/blog/uploaded_images/InstallingaMultiInstanceSQL2005Cluster_12B3D/clip_image00211_thumb.jpg)](http://www.ilmbestpractices.com/blog/uploaded_images/InstallingaMultiInstanceSQL2005Cluster_12B3D/clip_image00211.jpg)

6) Click Next after the System Consistency Checker or is it System Configuration Check (the SQL documentation vacillates between these two titles) is done

[![clip_image002[13]](http://www.ilmbestpractices.com/blog/uploaded_images/InstallingaMultiInstanceSQL2005Cluster_12B3D/clip_image00213_thumb.jpg)](http://www.ilmbestpractices.com/blog/uploaded_images/InstallingaMultiInstanceSQL2005Cluster_12B3D/clip_image00213.jpg)

7) Then click next

[![clip_image002[15]](http://www.ilmbestpractices.com/blog/uploaded_images/InstallingaMultiInstanceSQL2005Cluster_12B3D/clip_image00215_thumb.jpg)](http://www.ilmbestpractices.com/blog/uploaded_images/InstallingaMultiInstanceSQL2005Cluster_12B3D/clip_image00215.jpg)

8) Then click Maintain the Virtual Server. (Do not click Remove Microsoft SQL Server as this will uninstall the instance -- the virtual server).

[![clip_image002[17]](http://www.ilmbestpractices.com/blog/uploaded_images/InstallingaMultiInstanceSQL2005Cluster_12B3D/clip_image00217_thumb.jpg)](http://www.ilmbestpractices.com/blog/uploaded_images/InstallingaMultiInstanceSQL2005Cluster_12B3D/clip_image00217.jpg)

9) Then in the list of Selected Nodes select the node you want to remove from the Instance/Virtual Server. Click Remove and then click Next.

[![clip_image002[19]](http://www.ilmbestpractices.com/blog/uploaded_images/InstallingaMultiInstanceSQL2005Cluster_12B3D/clip_image00219_thumb.jpg)](http://www.ilmbestpractices.com/blog/uploaded_images/InstallingaMultiInstanceSQL2005Cluster_12B3D/clip_image00219.jpg)

10) After the uninstall is complete log off from the Node where you ran this and connect to the node you removed from the Instance/Virtual Server.

11) Then run the Install creating a new Failover Cluster.

When that is done, and before applying your SQL service packs, readd this node to the Instance/Virtual Server.

If this were a car repair manual I would simply say installation is the reverse of removal and no one would bat an eye. Instead I will give you a little more help:

Repeat steps 1-8

Then in the list of Available Nodes Select the node to be added and click Add. Then click Next.

[![clip_image002[21]](http://www.ilmbestpractices.com/blog/uploaded_images/InstallingaMultiInstanceSQL2005Cluster_12B3D/clip_image00221_thumb.jpg)](http://www.ilmbestpractices.com/blog/uploaded_images/InstallingaMultiInstanceSQL2005Cluster_12B3D/clip_image00221.jpg)

As the installation completes you will then receive a warning about needing to reapply service packs to the node you just added to the Instance/Virtual Server.

A reboot may be required on the node to be re-added. But if you wish to avoid it

### Additional Links and Articles

[Failover Cluster Troubleshooting](http://msdn.microsoft.com/en-us/library/ms189117(SQL.90).aspx "http://msdn.microsoft.com/en-us/library/ms189117(SQL.90).aspx") (I added some [Community Content](http://www.identitychaos.com/2008/08/microsoft-technetmsdn-community-content.html) to this page to see it go to the Failover article and scroll to the bottom)

[SQL Service Account needs to be in the group for Full Text Searching](http://support.microsoft.com/default.aspx?scid=kb;EN-US;917410)

[Troubleshooting Task Scheduler for your SQL Cluster Install](http://support.microsoft.com/kb/910851/en-us)

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices