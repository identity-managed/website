---
title: 'FIM 2010 hotfix available (4.0.3594.2)'
date: 2011-11-16T10:22:00.001-07:00
draft: false
url: /2011/11/microsoft-has-released-new-hotfix-kb.html
tags: 
- Forefront Identity Manager
- FIM
---

Microsoft has released a [new hotfix](http://support.microsoft.com/kb/2520954) (kb 2520954) at the end of October with some key fixes in it as well as one item that I will [blog about next](http://blog.ilmbestpractices.com/2011/11/ok-i-am-not-actually-swearing-nor-are.html) that prevents me from loading this on most implementations, until it is addressed.

Highlights

Component

Official Description

Comments

Workflow Engine (FIM Service)

Assume that you perform an operation that accesses the SQL database when the Microsoft SQL Server connection pooling feature is enabled in the FIM server. For example, you run a query or a request. If the operation times out for any reason, a future operation on the same thread may fail until that thread is removed from the SQL connection pool. An error message that resembles the following is displayed in the FIM Service Application event log, in the **RequestStatusDetails** property for a request, or in the **WorkflowStatusDetails** property of a workflow instance: Cannot enlist in the transaction because a local transaction is in progress on the connection.  
Additionally, the time stamp is the same as the time when the operation fails.

An operation on a thread that make a sql call that times out poisons the thread and all future operations on the thread fail.  
This could have lead to other problems that were hard to reproduce. Kudos on this one

Sync Engine

An **ExpectedRulesEntry** (ERE) object is associated to a child synchronization rule of a **Metaverse** object. If the ERE object has a **Remove** action, deprovisioning of the object is also being triggered. Then, the behavior causes the deletion of the **Metaverse** object

Much needed fix to ensure that deprovisioning doesn’t fire incorrecltly.

 

Fixes many "Export not reimported" errors that might occur because of errors in SQL.

Hallelujah – we see a fair amount of those. Would like to see more detail on that one

 

###### Improves the performance of all Sync Engine operations.  
**Note** This change involves an extensive upgrade to the sync database. This upgrade can take lots of time, depending on your hardware. A progress bar is displayed during the database upgrade.

Ok plan for a long time for your update. Be sure to back it up.  
  
This also sounds like a future blog article, to look a little deeper as to the changes.

 

###### Feature 2

The FIM 2010 Active Directory Management Agent (AD MA) does not honor the preferred domain controller list when passwords are exported. This is an issue for customers who require password changes to flow to a specific set of domain controllers. This hotfix rollup package changes the AD MA to use the preferred domain controller list first. If the preferred domain controller list does not exist, the domain controller locator service will identify a domain controller for password export operations. Additionally, you can still force password operations to use the primary domain controller by setting the following registry subkey:

Subkey:

HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\services\\FIMSynchronizationService\\Parameters\\PerMAInstance\\<MA\_name>

Value:  
UsePDCForPasswordOperations (REG\_DWORD, 1 = True, 0 = False)

This hotfix rollup package also updates the AD MA so that a trust relationship with the configured **Active Directory forest is not required to export passwords to that forest**.

This will be very helpful in large environments.  
  
Prior to this all password operations on FIM were targeting the PDC Emulator, which incidentally introduced a single point of failure.  
  
I also applaud the elimination of the need for the trust to do password exports!

 

###### Feature 3

Adds the ability to filter objects before they are imported into the AD MA connector space.

Another big win for large environments where we need to ignore large portions of the domain!

Sets and Query (FIM Service)

Fixes an issue that would sometimes cause incorrect Set calculations. This resulted in lots of set corrections. Also revised the Sets Correction job so that it does not change special sets that are maintained by another system maintenance job.

Thank you!

FIM MA

Fixes an issue in which the FIM synchronization service configuration for synchronization rules and codeless provisioning was not correctly written to the FIM Service database.

Seen this one. Glad to have a fix.

FIM Service

Fixes an issue in which unexpected data in the FIM Service database could result in the FIM MA causing the Synchronization service to fail during import, and a stopped-server error occurred.

Seen this one too.

 

###### Issue 4

Some **ExpectedRuleEntry** objects and **DetectedRuleEntry** objects in FIM 2010 can become "orphaned" over time. When a **DetectedRuleEntry** object is not referenced in the DetectedRulesList of any object in the system, that object is determined to be orphaned. Similarly, when an **ExpectedRuleEntry** object is not referenced in the ExpectedRulesList of any object in the system, that object is also determined to be orphaned.

Once more thank you.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices