---
title: 'Install ILM 2 in a SharePoint Farm'
date: 2009-04-16T17:40:00.001-07:00
draft: false
url: /2009/04/install-ilm-2-in-sharepoint-farm.html
tags: 
- Forefront Identity Manager
- FIM
- ILM 2 RC0
---

As I endeavored to install the ILM 2 Portal into a SharePoint farm (WSS 3.0 SP 1) with a remote database I encountered the following problem:

The dreaded Premature Failure during installation.

When I turned on logging for the install and examined the file, I found:

_Action 14:55:25: ConfigPortalAnonymousAccess._

_CAQuietExec:_ 

_CAQuietExec:  This operation can be performed only on a computer that is joined to a server farm by users who have permissions in SQL Server to read from the configuration database. To connect this server to the server farm, use the SharePoint Products and Technologies Configuration Wizard, located on the Start menu in Administrative Tools._

_CAQuietExec:_ 

_CAQuietExec:  Error 0xffffffff: Command line returned an error._

_CAQuietExec:  Error 0xffffffff: CAQuietExec Failed_

_Action ended 14:55:30: InstallFinalize. Return value 3._

_Action 14:55:30: Rollback. Rolling back action:_

So I turned on SQL Profiler and I noticed:

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/InstallILM2inaSharePointFarm_F742/image_thumb.png)](http://www.ilmbestpractices.com/blog/uploaded_images/InstallILM2inaSharePointFarm_F742/image.png)

So I decided to go ahead and give anonymous access (temporarily of course)

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/InstallILM2inaSharePointFarm_F742/image_thumb_3.png)](http://www.ilmbestpractices.com/blog/uploaded_images/InstallILM2inaSharePointFarm_F742/image_3.png)

Then I mapped the login to each of the three SharePoint databases and made it db\_owner.

Then my install worked perfectly. I hope to research and find out exactly which limited permissions are needed.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices