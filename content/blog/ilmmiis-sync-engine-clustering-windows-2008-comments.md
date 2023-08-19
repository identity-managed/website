---
title: 'ILM/MIIS Sync Engine Clustering Windows 2008'
date: 2009-03-16T10:31:00.001-07:00
draft: false
url: /2009/03/ilmmiis-sync-engine-clustering-windows.html
tags: 
- Clustering
- ILM
- Windows Server 2008
---

#### David,  
  
I can't figure this one out easily s...
[Anu](https://www.blogger.com/profile/16607719880402498029 "noreply@blogger.com") - <time datetime="2009-03-30T13:15:00.000-07:00">Mar 1, 2009</time>

David,  
  
I can't figure this one out easily since I don't have a deep knowledge of SQL. I'd appreciate your feedback. I am beginning to understand the different options and implementaions for scaling out SQL HA/DR/automatic failover.  
  
In ILM "2" architecture, with scaling out MIIS and its SQL, can performace improvements and concurrent MA runs be achieved? I think not but I'd like to wrong this time!  
  
Thanks.  
Regards,  
Anu Melkote
<hr />
#### Concurrent synch MA runs cause issues with locking...
[David Lundell](https://www.blogger.com/profile/17202883653808140101 "noreply@blogger.com") - <time datetime="2009-04-08T16:04:00.000-07:00">Apr 3, 2009</time>

Concurrent synch MA runs cause issues with locking since synching one CSentry might access a csentry in another MA.  
  
With ILM 2 you can load balance by separating the sync engine db and the ilm ws db
<hr />
#### Hi Guys, I have taken the opportunity to update A...
[Damian Flynn](https://www.blogger.com/profile/14734548745865746892 "noreply@blogger.com") - <time datetime="2012-10-11T04:24:30.420-07:00">Oct 4, 2012</time>

Hi Guys,  
I have taken the opportunity to update Alex's script for creating a HA FIM 2010 R2 Cluster and created an end to end guide  
http://www.damianflynn.com/2012/10/11/fim-sync-server-2010r2-cluster-build/  
  
thanks  
Damian
<hr />
