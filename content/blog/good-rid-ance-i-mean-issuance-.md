---
title: 'Good RID(ance, I mean issuance)'
date: 2014-04-16T08:45:00.001-07:00
draft: false
url: /2014/04/good-ridance-i-mean-issuance.html
---

As we know a SID is 12 Bytes long or 96 bits long and is composed of several components, among them the domain identifier and the relative identifier or RID of a particular object. The RID is 30 bits long which means you have approximately 1 billion RIDs. So while you think it is unlikely that you will run out of RIDs, according to [http://TechNet.microsoft.com/en-us/library/jj574229.aspx](http://technet.microsoft.com/en-us/library/jj574229.aspx) you can encountering this if you have accidentally used scripts or provisioning tools (like FIM) to shoot your self in the foot and create gobs and gobs of users, you let some end-user go out of control creating waaaay too many groups, you increased the RID pool size to be too big, did lots of DC demotion and promotion, cleanups, forest recoveries or invalidated RID pools.  
  
In short most of you would be more likely to encounter this in a test or dev environment where you destroy and create many many users as part of your testing with FIM.  
  
So Windows Server 2012 to the rescue.  
1) It adds a bit so now you can unlock that bit and have 31 bits for the RID or 2 billion RIDs.  
2) You get warnings in the event log whenever you consume 10% of the space left since your last warning.  
3) Now there is a safety mechanism, you can't increase the RID Block size to higher than 15,000. Previously there was no limit and you could have allocated the entire RID space in one transaction to one domain controller.  
4) There are also brakes. When you are within 1 percent of only have 10% of your global RID space left you get warned and there is also an artificial ceiling so that you can fix whatever is chewing up your RIDs before you are out.  
  
In short good RID(ance I mean issuance).

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices