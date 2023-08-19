---
title: 'Hints of FIM''s Future: Azure Active Directory (AAD) Sync'
date: 2014-04-17T08:19:00.000-07:00
draft: false
url: /2014/04/hints-of-fims-future-azure-active.html
tags: 
- FIM 2010 R2
- Azure
- AAD
- Office365
- FIM
---

For years I have been trying to predict the future of Identity Management, but every time I look in my crystal ball it is just too cloudy to see anything. In fact anytime I look in my crystal ball on just about any technology topic the only thing it shows me are clouds! I was beginning to think it was broken.  
  
But then, yesterday, I watched Andreas Kjellman present at the FIM user group  
Andreas unveiled the AADSync, the Azure Active Directory Sync that will replace DirSync to sync from your Active Directory to the cloud. I finally got it! My crystal ball wasn't broken!  
  
AADSync is built on the next generation of the Sync Engine. 80% of the scenarios for syncing with Azure (Office365) will be handled with a wizard, including Multi-Forest. For more advanced scenarios you will be able to use a significantly upgraded function library to do "declarative provisioning" with sync rules. In fact no code for rules extensions will be permitted.  
  
What does this mean for FIM?  
  
I speculate that eventually FIM will follow this path. Since this next version seems to support the same connector framework, I think we will continue to see connector development as well as continued cloud capabilities ala Azure Access Enhancements and Azure AD Premium.  
  
Thanks to the user group sponsor --  the FIM team, hosted by Carol Wapshere for putting it together and eventually providing the recording found here: [http://thefimteam.com/fim-team-user-group/](http://thefimteam.com/fim-team-user-group/)  
  
AADSync is available now in Preview.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices