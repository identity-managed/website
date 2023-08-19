---
title: 'New version PCNS, new FIM hotfix'
date: 2012-08-30T09:59:00.001-07:00
draft: false
url: /2012/08/new-version-pcns-new-fim-hotfix.html
tags: 
- Forefront Identity Manager
- FIM 2010 R2
- Passwords
- FIM
---

On Aug 24th Microsoft released a new version of PCNS. Version number 4.1.2515.0.

No release notes are provided with the download. However, this version number matches the version number of the latest FIM R2 hotfix rollup [http://support.microsoft.com/kb/2734159](http://support.microsoft.com/kb/2734159 "http://support.microsoft.com/kb/2734159") and it does tell us what is fixed:

> Assume that you run Password Change Notification Service (PCNS) setup together with the **SCHEMAUPDATE=TRUE** option and the schema is updated successfully. In this situation, an error message is displayed at the end of the setup process incorrectly.  
> After this update is installed, the Setup program does not display the error message when the schema update is successful.

It should be noted that this FIM hotfix is only for FIM 2010 R2 (version 4.1.2273.0)

Apparently there were some issues with unicode characters for usernames in the FIM Portal and folders and filenames with unicode characters that the Sync Service used.

FIM Sync had a problem with deleting AD users that had active sync devices added to their account – solved!

Full import on a large connector space was sometimes having a problem with obsoletion and getting an error “0 is not a valid DN depth”

There have also been some issues with the upgrade to R2 failing while trying to upgrade the sync engine. They now have a tool that you can get from support to work around the failure by upgrading the database separately.

The hotfix solves a problem introduced by R2 (build 2273) incorrect removal of members from sets and groups where the filter looks like: /Person\[(FirstName=”John”) or (FirstName=”Bill)\]

There is even a fix for FIM certificate management “to improve error messages handling.”

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices