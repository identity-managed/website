---
title: 'To Farm or not to Farm Part 2'
date: 2018-03-29T17:43:00.000-07:00
draft: false
url: /2018/03/to-farm-or-not-to-farm-part-2.html
tags: 
- #FIM
- #MIM
- #SharePoint
---

In the original [To Farm or Not to Farm post](http://blog.ilmbestpractices.com/2014/05/to-farm-or-not-to-farm-that-is-question.html) I discussed the pros and cons of setting up FIM on a SharePoint farm or using Stand Alone. Well we now have SharePoint 2016 and it isn't possible to install Stand Alone, although you can do a single server farm. Also, absolutely everything is virtualized and so we tend to share lots and lots of processing so we can't really think of a server as having spare cycles, because we share those processors with lots of other VM's.  
  
This first point got me thinking and the last point now has me convinced that we shouldn't do Stand Alone on SharePoint 2013 Foundations or any other, because it adds the overhead of SQL Express when we can get better overall performance by using the real SQL Server, even if the SharePoint databases share it with all of the MIM databases. However, the patching issues brought up by [Paul Williams](http://blog.msresource.net/2013/05/16/editing-the-fim-portal-web-config-in-a-farm-topology/) are still real.  
  

I think a lot of people have been sticking with the free option -- SharePoint Foundations 2013. Which is  [possible to install on Windows Server 2016](https://social.technet.microsoft.com/Forums/en-US/645cd193-afb3-4c5b-9126-8284c3491603/roger.dilsner.com/install-sharepoint-foundation-2013-windows-server-2016-solution/) even if it is not exactly supported. So a lot of folks have avoided thinking about SharePoint. Here are some points to consider

1.  The challenge has to do with the way MIM does its updates. If you separate MIM Service from the MIM Portal then you are better off when it comes to the MIM updates if you are in a multi-server farm.
2.  I have not seen any guidance from Microsoft Identity about what roles are needed in SharePoint 2016. However, it appears to me that the MIM solution is essentially a content farm which per[MSFT would require 3 roles or 2 servers with shared roles, or the single server farm](https://docs.microsoft.com/en-us/SharePoint/install/planning-for-a-minrole-server-deployment-in-sharepoint-server-2016): Front End, Application and Distributed Cache.
3.  For Zero Downtime patching to apply you need to be in a Highly Available solution. With Min Role that takes 4 servers. Unfortunately, I don't know if that will allow you to update the MIM solution pack without downtime. One of the changes that the SharePoint team made is to keep stored procedures in the SharePoint databases backwards compatible. I don't think the MIM product group has made any such guarantees. So when we patch MIM Service it will update the database and the MIM Service. At that instant only updated MIM Service instances should talk to the database (they might work, but no guarantees), and only updated Portals should talk to the update MIM Service Instance. So I think we still end up with downtime, the key is to minimize it. The Zero downtime patching would certainly reduce it when you patch the actual SharePoint binaries. But we could accomplish the same thing with two single server farms load balanced through NLB.

  

Anyone else have any thoughts or experiences to share?

So for now, I recommend essentially a single server farm on SharePoint 2013 Foundations, and to use your own variant of [Spencer Harbar's scripts to configure it.](http://www.harbar.net/articles/fimportal.aspx) If you want to do that don't check this box:  
  

[![](https://3.bp.blogspot.com/-9qPRGO6pKeE/Wr2HqUmP3MI/AAAAAAAAALI/7Zx26EmfIVkuQv2garor9fsoInGihOxzwCLcBGAs/s320/Run%2BSharePointConfig%2BWizard.png)](https://3.bp.blogspot.com/-9qPRGO6pKeE/Wr2HqUmP3MI/AAAAAAAAALI/7Zx26EmfIVkuQv2garor9fsoInGihOxzwCLcBGAs/s1600/Run%2BSharePointConfig%2BWizard.png)

  

For HA: deploy another one (be sure to use different database names) and then load balance.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices