---
title: 'SharePoint MA -- avoid the noise'
date: 2016-06-28T19:47:00.001-07:00
draft: false
url: /2016/06/sharepoint-ma-avoid-noise.html
tags: 
- Forefront Identity Manager
- MIM
- FIM
- SharePoint
---

In using the [SharePoint MA from Steve Kean](http://social.technet.microsoft.com/wiki/contents/articles/1589.fim-2010-management-agents-from-partners.aspx#SharePoint_List_Management_Agent_from_Steven_Kean_at_Version3) I noticed that some of the fields I imported were coming in with some extra noise or crap at the beginning:  
  
String;#164  
  
All I really wanted was the 164. While I can use the Word function in a sync rule to get past it  
Word(strAttribute,2,"2") I really would prefer to bypass it altogether.  
  
Well thanks to Jermaine Snipe I found why this happens and how to bypass it:  
These are calculated columns and they use the concatenate function. Instead use a Text formula for the calculated column. This of course supposes that you can get the SharePoint developer to change it.  
  

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices