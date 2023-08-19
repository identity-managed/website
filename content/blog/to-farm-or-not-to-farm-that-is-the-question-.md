---
title: 'To Farm, or not to Farm, that is the question --'
date: 2014-05-01T12:37:00.001-07:00
draft: false
url: /2014/05/to-farm-or-not-to-farm-that-is-question.html
tags: 
- Forefront Identity Manager
- FIM 2010 R2
- FIM
- SharePoint
---

*   Whether 'tis nobler in the mind to suffer
*   the slings and arrows of outrageous fortune
*   Or to take **Farms** against a sea of **patches**
*   and by opposing end them? To, die, to sleep --

Today I will be "moderating" the debate about using SharePoint Farms vs. Stand-Alone as the foundation for the FIM Portal. In this corner we have [Paul Williams of Microsoft](http://blog.msresource.net/) sharing knowledge from [his hard fought victories with FIM](http://blog.msresource.net/2013/05/15/fim-portal-in-a-sharepoint-farmwhy-you-should-not-do-this/) and [painful experiences with Farms](http://blog.msresource.net/2013/05/16/editing-the-fim-portal-web-config-in-a-farm-topology/). In the other corner we have [Spencer Harbar](http://www.harbar.net/), SharePoint MVP, applying his years of [SharePoint expertise to the FIM world](http://www.harbar.net/articles/fimportal.aspx) providing a [definitive guide to installing FIM 2012 R2 SP1 portal on SharePoint 2013](http://www.harbar.net/articles/fimportal.aspx).

Spencer points out that "farm deployment aspects are generally not well understood by FIM practitioners which leads to a number of common deployment and operational challenges." **Point conceded.** I saw much of the same thing with regards to MIIS and ILM when it came to deploying SQL Server.

Spencer argues that "the general idea is to build a small dedicated SharePoint instance purely for the purposes of hosting the FIM Portal \[and FIM Service\] and **nothing else** (although it could also host the Password Registration and Reset web sites)" and that by deploying a farm instead of Stand-Alone, the "craptastic demoware default configuration,"  you can avoid "a bunch of unnecessary goop."   _Note: Assuming Spencer knows, but just to clarify for everyone, the Password Portals use IIS and do not need or use SharePoint._

An example of the "unnecessary goop" is the SharePoint Search Service Application, which when installed then requires us to turn off the SharePoint Indexing job. A benefit of avoiding "a bunch of stuff we don’t want" is that it "minimizes the attack surface available." **Minimizing attack surface is a good thing.**

Spencer opines that "the Standalone Server Type... is evil, pure and simple." He also decries the use of "Embedded SQL."

Paul shares some compelling experience based evidence to think about using Stand-Alone instead of a farm, stating that a farm gives you a "**serious headache when patching** ... more operational maintenance" (more SQL Server Databases to manage instead of the "optimised WID\[embedded SQL\] files that are totally expendable")  "and more complexity around backup and restore (or rebuild) and patching SharePoint itself" not to mention when you need to "\[modify\] web.config."

Patching needs to be explored further. According to Paul, you must "patch ... nodes sequentially" which "takes quite a bit longer than a standalone node" because "the FIM installer isn’t optimised for a farm" which would normally "deploy the solution pack once" instead we have an installer for the FIM Service and Portal, meaning the patch is the same. Since you need to patch the FIM Service on each node you must run the patch on each node which will also see the FIM Portal, "retract the solution pack and deploy the new one," which in turns causes "all application pools related to SharePoint to be recycled." Since "the retraction and redeployment is global (to SharePoint)" that means "that downtime affects all nodes in the farm – you can’t drop one out of the NLB array, patch, add back, drop the next, etc." Whereas if you do Stand Alone you can "drop one out of the NLB array, patch, add back, drop the next, etc."

I know that with some of the pre-R2 updates I have been able to run the patch on the first node of the farm, installing FIM Service and Portal, and then on the second node just installing the patch for the FIM Service, since the Portal bits had already been updated. I need to double check whether this is still the case (since then most of our installs have been stand-alone).

Paul continues with the woes of the Language packs that  they "comprise some file system files for the FIM Service and SharePoint solution packs," which for a Farm means repeated downtime for the whole farm as each node is Language Packed. If you need language packs then a farm is still bad news for downtime even if the method I have used still applies for the Service Pack and hotfixes.

**Pros for SharePoint Stand-alone for FIM**

**Pros for SharePoint Farm for FIM**

**Setup is simple** (it creates the first site collection, plus database and site for you)

Can get much **smaller attack surface** by not installing "unnecessary goop"

Don't have to have a separate SQL Instance (which you must make highly available to avoid single point of failure) to manage, backup, etc.

Avoid the overhead of running the Windows Internal Database/SQL Express Edition (aka Embedded SQL) on each node (overhead that we haven't seen cause FIM performance issues).

**Can patch one server at a time without taking down whole NLB Array** of FIM Servers (also each node is faster to patch)

Can deploy pure SharePoint items and CSS files once instead of to each node

Perhaps there are ways to get the most of the best of both worlds.

1.  Install one Single Server SharePoint Farm for each FIM Portal node

1.  Upside: You avoid the painful patching process and Language Pack process
2.  Upside: Done right have the smaller attack surface (you would get complete control)
3.  Downside: More complex installation, but you could use the very complete scripts from Spencer to do this
4.  Downside: Shoot where do I want to put all those databases? I could put them on the SQL Server that will host the other FIM databases

3.  Separate the FIM Service from the FIM Portal

1.  Upside: This way when you do the patching and language packs that impact the portal they should only need to be done once, but still have downtime for whole farm.
2.  Upside: Smaller attack surface
3.  Upside: Pure SharePoint items and CSS files get deployed and configured only once
4.  Downside: more vm's/machines to manage and more FIM Server licenses to buy

5.  Install Stand-Alone and find a way to reduce the "attack surface" by eliminating some of the "unnecessary goop"

1.  This has most of the upsides and few of the downsides if we can find a way to do it
2.  Spencer: This is where I would love to have your expert opinion: How to reduce the attack surface on SharePoint Stand-Alone.

Conclusion: Initially, working with Brad Turner, I went with Farms, but then when I saw the Language Pack issues I thought Stand-Alone. Also when trying to keep it simple for non-SharePoint Admins, I thought Stand-Alone. As always there are trade offs, and want to see more discussion before we settle on single answer or even a definitive decision tree for which one to choose. For now I lean towards each FIM Portal and Service node having its own SharePoint Stand-Alone instance, but would love to advance the state of the art with better security and possibly performance.

**All: Give me your thoughts on one vs. the other or on the additional options.**

Note: Ross Currie also provides a [guide resulting from his hard fought battle to get FIM on SharePoint 2013](http://www.fimspecialist.com/fim-portal/installing-fim-2010-r2-sp1-portal-on-sharepoint-foundation-2013/)

Note: Paul and Spencer AFAIK have never actually carried out a debate on this topic.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices