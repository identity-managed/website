---
title: 'MIM 2016 SP1 -- Implications'
date: 2016-10-19T04:18:00.002-07:00
draft: false
url: /2016/10/mim-2016-sp1-implications.html
tags: 
- Microsoft Identity Manager
- MIM
---

Earlier this month Microsoft [released MIM 2016 SP1](https://docs.microsoft.com/en-us/microsoft-identity-manager/understand-explore/microsoft-identity-manager-2016-sp1-release-notes)  
But what does this mean for you?  
  
Biggest Implications  
  
  

1.  Exchange Online (Office365) for the MIM Service 

1.  without losing the ability to approve requests from within Outlook, and the requesting of groups within Outlook.

1.  Since lots of orgs are using Office 365 no more embarrassing conversations about these great features you can't have.

3.  Support for other browsers for MIM Portal

1.  SSPR already supported other browsers but now MIM Portal will support Chrome, Firefox and Safari.

1.  This means less customer resistance

5.  [Platform Support](https://docs.microsoft.com/en-us/microsoft-identity-manager/plan-design/microsoft-identity-manager-2016-supported-platforms) -- MIM now supports all of the latest platforms Windows 2016, Active Directory 2016, SQL 2016, SharePoint 2016, Exchange 2016.

1.  Sync, Service and Portal

1.  Can now run on these

3.  Portal can now run on SharePoint 2016

1.  But there is not a foundations version meaning a free version

1.  So keep running on SharePoint 2013 Foundations for now unless MSFT starts including a license for SharePoint 2016

5.  [SharePoint 2016 no longer uses FIM/MIM](http://hey%20now%20have%20active%20directory%20import/) 

1.  You can use MIM, but the default is the new built in Active Directory Import
2.  If you do use MIM to synch to SharePoint check [Spencer Harbar's notes](http://www.harbar.net/archive/2016/10/06/Microsoft-Identity-Manager-2016-Service-Pack-1-is-now-available.aspx)

7.  BHOLD

1.  The [supported platform page](https://docs.microsoft.com/en-us/microsoft-identity-manager/plan-design/microsoft-identity-manager-2016-supported-platforms) lists that with MIM 2016 SP1 BHOLD now supports SQL 2014

1.  Say what? Why not SQL 2016? is this an error? If true this implies that BHOLD isn't as highly prioritized.

9.  MIM Certificate Management

1.  Lists the only supported client as Windows 7

1.  Again -- if true this suggest lower priority. In general most new MFA solutions aren't using smart cards and certs.

11.   PAM now supports Windows Server 2016 and forest functional level 2016

1.  Kerberos tickets are now time limited based on the time left on your role activation

1.  Improved security!

Finally, look at [Jorge's screenshot by screenshot post on how to upgrade](https://jorgequestforknowledge.wordpress.com/2016/09/26/upgrading-to-mim-2016-sp1/)

  
  

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices