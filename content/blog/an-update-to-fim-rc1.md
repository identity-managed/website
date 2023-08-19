---
title: 'An Update to FIM RC1'
date: 2009-11-08T23:14:00.001-07:00
draft: false
url: /2009/11/update-to-fim-rc1.html
tags: 
- Identity Management
- FIM
---

Microsoft has posted an update to FIM RC 1, dated Nov 6.

It looks like this update covers pretty much everywhere except Certificate Services (sorry Brian and Paul).

The Release notes included in the download lists the follow improvements:

*   Query and Sets

*   Resolved a number of issues that resulted in incorrect dynamic set membership.
*   Removed support for the use of the != operator with multivalued attributes. Xpath equality expressions on multivalued attributes must use the not() function.  For example, the following xpath is not supported: /Group\[Owner != /Person\].  Instead, use the following xpath: /Group\[not(Owner = /Person)\]

*   Synchronization engine

*   Resolved a data corruption issue in Multi-Mastery scenarios where deleted Member attributes were being added back during full sync of AD and FIM.

*   Workflows

*   Workflows are now run on a FIM Service that uses the same ExternalHostName as the FIM Service that originally created the workflow. This enables the partitioning of workflow execution among servers dedicated to specific functionality.   
    For example, if a FIM Service is dedicated to servicing Requests submitted by the Synchronization Service, all workflows resulting from Synchronization Service Requests will only run on that FIM Service.
*   Resolved an issue that caused a Request’s RequestStatus attribute to retain the value “Validating” even though the Request’s operation timed out.
*   Resolved an issue in the EnumerateResourcesActivity that prevented selecting which attributes to return. Previously, regardless of the attribute selection specified, all attributes bound to the enumerated resources were returned.

*   Resolved various issues and made general improvements for:

*   Management Policy Rules
*   Portal user interface Request Management
*   Self-service Password Reset
*   Schema

Some of those items raise a few questions, like how to setup a FIM service that only takes requests from the sync service? Do we setup multiple FIM Service instances and then configure the FIM MA to talk to one of them, and not make that one available to web clients?

Go to Connect.microsoft.com and 11/6/2009  
Here’s the link: [FIM 2010 RC1 Update 1](https://connect.microsoft.com/Downloads/DownloadDetails.aspx?SiteID=433&DownloadID=23207)  
4.0.2570.0 (compare to 4.0.2560.0 the version released on 9/29/09 -- RC1)  
Build

It references a KB article that I can’t find: KB976465

The total download is under 36 MB so this is definitely a patch and not the full enchilada.

[Looks like Jorge got the news out first.](http://blogs.dirteam.com/blogs/jorge/archive/2009/11/08/update-release-for-fim-2010-rc1.aspx)

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices