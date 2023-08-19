---
title: 'Is MIM dead? Not yet!'
date: 2017-03-29T08:17:00.000-07:00
draft: false
url: /2017/03/is-mim-dead-not-yet.html
tags: 
- Microsoft Identity Manager
- Identity Management
- SailPoint
- MIM
- FIM
- BHOLD
---

From time to time I hear people wonder if MIM is dead.  
  
Why do people ask?  
  

*   They don't feel like they have heard a good road map recently
*   They aren't seeing the improvements they hoped for
*   They aren't paying attention to the actions of the product group

Why do I say it isn't dead yet?

*   While the Cloud Identity is the future, we are and will be in hybrid identity for a long time and MIM is Microsoft's key component to that.
*   I look the product group investments -- while of course they continue to enhance the cloud based capabilities of Azure AD they also [continue to fix and enhance MIM](https://social.technet.microsoft.com/wiki/contents/articles/32507.mim-2016-build-overview.aspx#Build441459)

*   With MIM they added Privileged Account Management -- Aug 2015
*   Hotfix in Dec 2015
*   Hotfix April 2016
*   Hotfix July 2016
*   [SP1](https://docs.microsoft.com/en-us/microsoft-identity-manager/understand-explore/microsoft-identity-manager-2016-sp1-release-notes) in Oct 2016 (but use the [hotfix from Nov](https://support.microsoft.com/en-us/help/3201389/a-hotfix-rollup-package-build-4.4.1302.0-is-available-for-microsoft-identity-manager-2016))
*   The [latest hotfix](https://support.microsoft.com/en-us/help/4012498/hotfix-rollup-package-build-4-4-1459-0-is-available-for-microsoft-iden) was just two days ago with not just fixes but several bonafide enhancements (4.4.1459.0):

*   [SQL Always On Support](https://t.co/SmXZ0hmb3P)
*   [The ability to have custom objects with membership similar to Groups and Sets](https://t.co/wUVcxzUYNi)
*   [Enter a justification on Approval not just denials](https://t.co/i4SnAYeFdw)
*   [The ability to turn on and off logging for the MIM Service without having to restart](https://blogs.technet.microsoft.com/iamsupport/2017/03/27/microsoft-identity-manager-2016-sp1-portal-4-4-1459-0-or-later-support-for-fimservice-dynamic-logging/)
*   [Support for SCCM 2016](https://blogs.technet.microsoft.com/iamsupport/2017/03/27/microsoft-identity-manager-2016-sp1-portal-4-4-1459-0-or-later-support-for-scsm-2016-reporting/) for Reporting
*   Updated article to include CM
*   [Certificate Modern Manager](https://www.microsoft.com/en-us/download/details.aspx?id=54954)

*   [Improvements to PIN Verification](https://support.microsoft.com/en-us/help/4012498/hotfix-rollup-package-build-4-4-1459-0-is-available-for-microsoft-iden)

It is possible that BHOLD components of MIM are dying or at least of lesser import. Biggest evidence for this is [Microsoft's partnership with SailPoint](https://redmondmag.com/articles/2017/02/13/sailpoint-and-azure-active-directory.aspx) coupled with the fact that there are no BHOLD fixes in the latest hotfix.  
  
Update: I have been reassured by the product group that BHOLD will continue to get development for fixes and new features.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices