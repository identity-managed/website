---
title: 'MIM 2016 is now available'
date: 2015-08-04T08:12:00.000-07:00
draft: false
url: /2015/08/mim-2016-is-now-available.html
tags: 
- Forefront Identity Manager
- FIM 2010 R2
- Microsoft Identity Manager
- MIM
- FIM
---

[MIM 2016 is now available](http://www.microsoft.com/en-us/server-cloud/products/microsoft-identity-manager/)  
  
MIM -- Microsoft Identity Manager 2016 builds on and replaces Microsoft's Forefront Identity Manager 2010 R2.  
  
On Microsoft's site they include an [introductory (2 min) video about Hybrid Identity](https://www.youtube.com/embed/65ueuS3-wTQ) but don't mistake that for the MIM UI.  
  
**So has anything been removed?**  
  
No. While the list of deprecated features are still deprecated none of them have been removed from this new version.  
  
**So what's new?**  
  
The first thing to call your attention is the focus on Hybrid (Cloud + On Premise) Identity. MIM can still manage on premise but is now even better equipped to work with Microsoft's Identity Management pieces in the cloud.  
  
PAM -- Privileged Account Management. You establish a secure Forest (a bastion forest) with MIM deployed there and you request temporary membership in a role that then puts you in a group in the bastion forest that grants you elevated privileges in your main forest(s). Microsoft's take on this is different than others such as CyberArk which vault your privileged passwords and change them frequently.  
  
SSPR -- Self Service Password Reset can now use Azure MFA (Phone Factor)  
  
Self Service Unlock -- Use the SSPR mechanisms to authenticate and then unlock your account without resetting the password. Useful when you change you password but forget to update the cached password on your phone.  
  
Certificate Management -- Win 8.1 client, no need to join to the domain (if using ADFS), Virtual Smart card, claims, events for troubleshooting.  
  

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices