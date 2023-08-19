---
title: 'Top 11 new features of FIM 2010 R2 SP1'
date: 2013-01-15T20:25:00.001-07:00
draft: false
url: /2013/01/fim-2010-r2-sp1-documentation-and-bits.html
tags: 
- Forefront Identity Manager
- FIM 2010 R2
- FIM
---

My comments on What's new and the release notes for FIM 2010 R2 SP1:

Rank

Feature

Impact

1

[Deferred evaluation of criteria based groups](http://technet.microsoft.com/en-us/library/jj863243(v=ws.10).aspx)  
This setting can be enabled one group at a time. You can also change the default so that as new criteria based groups are created they will be set for Deferred. The default is to calculate group membership twice a day at 2:30 AM and 2:30 PM.

HUGE! Thank you product group for answering my wishes. You see whenever a request is received by the FIM Service it evaluates permissions, it evaluates whether the request will cause any criteria based set memberships to change, and it also evaluates whether criteria based group memberships to change. For large systems with lots of users and lots of criteria based groups this can take a long time.Now we have the option to defer those calculations, and then the system can perform those calculations using SQL based set logic. I suspect that this is done using SQL Agent jobs and if a more frequent schedule is needed you could tweak the schedule of the job.

2

Upgrading the FIM database from FIM 2010 to R2 used to be quite time consuming -- this has been improved by at least an order of magnitude from "days \[down\] to hours."

Phew! It is now safe to get up and upgrade!

3

"imports of groups with 30,000 members are 2.5 times faster" for AD MA, FIM MA and ECMA 2.0

This is on the import side rather than the sync side but every bit of additional speed we get on dealing with references without sacrificing integrity is appreciated.

4

ECMA has been updated to 2.1

You can now do updates on multi-valued attributes instead of having to do a replace.  
  
You can also skip doing confirmations on add.  
Good impact on performance

5

FIM Server components are now supported for:  
Windows Server 2012  
SQL 2012  
SharePoint Foundation 2013 (read [Installing FIM 2010 R2 on SharePoint Foundation 2013](http://technet.microsoft.com/en-us/library/jj863242(v=ws.10).aspx).)  
SCSM 2012

Note support for earlier versions hasn't been dropped yet.

6

FIM Client components are now supported for:  
Windows 8  
Outlook 2013

Note support for earlier versions hasn't been dropped yet.

7

Support for Windows Server 2012 based AD and Exchange 2013 has been added to the AD MA

Note support for earlier versions hasn't been dropped yet.

8

Support for SQL Server 2012 has been added to the SQL MA

Note support for earlier versions hasn't been dropped yet.

9

Support for the FIM Portal in IE 10 (be sure to install the hotfixes mentioned)

*   Windows Server 2008: [http://support.microsoft.com/kb/2600100](http://support.microsoft.com/kb/2600100)
*   Windows Server 2008 R2: [http://support.microsoft.com/kb/2608565](http://support.microsoft.com/kb/2608565)

10

The Sun and Netscape MA is now called Oracle Directory Servers and includes support for Sun 7.x and Oracle 11

Support for Oracle Internet Directory 11g!!!

11

"Import-MIISServerConfig PowerShell cmdlet supports now overwriting an existing configuration"

This will help with automated testing scenarios!

Source Articles:

[What's New in Forefront Identity Manager 2010 R2 SP1](http://technet.microsoft.com/en-us/library/jj863246(v=ws.10).aspx)

[Release Notes for Forefront Identity Manager 2010 R2 SP1](http://technet.microsoft.com/en-us/library/jj863245(v=ws.10).aspx)

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices