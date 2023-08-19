---
title: 'ILM/MIIS Sync Engine Clustering Windows 2008'
date: 2009-03-16T10:31:00.001-07:00
draft: false
url: /2009/03/ilmmiis-sync-engine-clustering-windows.html
tags: 
- Clustering
- ILM
- Windows Server 2008
---

First, let me say thank you to [Alex Tcherniakhovski](http://blogs.msdn.com/alextch/default.aspx) for pioneering the way in clustering the MIIS Service or as it is now known the ILM Sync Engine. That blog, presentation and script was an excellent set of work. [http://blogs.msdn.com/alextch/archive/2005/12/17/clusteredmiis.aspx](http://blogs.msdn.com/alextch/archive/2005/12/17/clusteredmiis.aspx "http://blogs.msdn.com/alextch/archive/2005/12/17/clusteredmiis.aspx")

On Windows Server 2008, a few things have changed that break the script that Alex T. provides.

In Windows Server 2003 the cluster services runs as a domain account and as long as the user has access to all nodes, to stop and start services, and as an MIIS Administrator then it should be able to do the trick.

Well with Windows Server 2008 the security model for the cluster service has changed:

[http://support.microsoft.com/kb/947049](http://support.microsoft.com/kb/947049)

[http://technet.microsoft.com/en-us/magazine/2008.07.failover.aspx](http://technet.microsoft.com/en-us/magazine/2008.07.failover.aspx)

There is no service account, instead there is a Cluster Name Object created in AD as a computer object.

So the cluster service, which runs the generic resource scripts, now runs under local system in a special context with limited privileges.

So this means you can’t impersonate during WMI calls because it doesn’t have enough rights.

I tried making the CNO a member of the local administrators group, but that wasn’t enough. I may still get this to work.

For the mean time I am switching the remote wmi calls to use embedded credentials, but the local WMI calls can't have credentials like so:

if Node = activeNode Then

Set objWMIService = objSWbemLocator.ConnectServer(Node, \_

    "root\\CIMV2")

Else

Set objWMIService = objSWbemLocator.ConnectServer(Node, \_

    "root\\CIMV2", \_

    strUser, \_

    strPassword, \_

    "MS\_409", \_

    "ntlmdomain:" + strDomain)

End If

After changing this several places in the code -- fixing how the command to sleep worked, I can now failover without a problem!

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices