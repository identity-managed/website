---
title: 'Final Update for FIM RC1 released'
date: 2010-02-01T10:40:00.001-07:00
draft: false
url: /2010/02/final-update-for-fim-rc1-released.html
tags: 
- Forefront Identity Manager
- ILM
- Identity Management
- FIM
---

On Friday the product group released Update 3 for Forefront Identity Manager 2010 RC1 available through connect

[https://connect.microsoft.com/site433/Downloads](https://connect.microsoft.com/site433/Downloads "https://connect.microsoft.com/site433/Downloads")

Major changes as part of Update 3 (my regurgitation and comments from the release notes):

*   Fewer trips to the FIM Service event log – since the FIM MA export errors will now show up in the Synchronization Service Manager! Hallelujah!
*   Less need for custom old style code
    *   Now more than 1 MA can be authoritative for deleting an object (resource)
    *   New functions for Sync Rules (Declarative Provisioning) – I guess I will have to update [my function cheatsheet](http://www.ilmbestpractices.com/blog/2009/01/ilm-2-functions-explained.html)
        *   Null – not certain what they mean by this – null out the value or let another sync rule provide the value.
        *   ReplaceString
*   New type of MPR – Set Transition MPRs vs. request based MPRs
    *   Run on Policy Update only applies to this type
    *   All other MPRs are – request based MPRs
    *   This should easy some of the difficulty in wrapping heads around MPRs.
*   DBA’s will love these:
    *   Backups without stopping the FIM Service and now supported!
    *   SQL Failover Clusters are now supported! (I don’t know if this means that clustering the Synchronization Service is supported)
*   Prereqs have changed
    *   Server Components
        *   Windows Installer 4.5 is required,
    *   FIM Service requires SQL 2008 SP 1
    *   The addin for Outlook now needs Outlook 2007 SP 2

Even the certificate management side got some improvements: Windows Server 2008 R2

[Also check out Brad’s post on the SP3 for MIIS or an update to ILM 2007 FP 1](http://http://www.identitychaos.com/2010/01/ilm-2007-fp1-service-pack-1-build.html)

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices