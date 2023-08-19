---
title: 'Processing Actions Asynchronously outside of ILM MA''s'
date: 2008-05-15T06:25:00.004-07:00
draft: false
url: /2008/05/processing-actions-asynchronously.html
tags: 
- Microsoft Message Queue
- ILM
- MSMQ
- SQL Server Service Broker
- SQL Server
- SSB
---

For years developers have had access to the Microsoft Message Queue (MSMQ) as a way to be able to queue up actions for processing later or on a remote machine. With the release of SQL 2005 back in well 2005, developers with access to SQL 2005 could replace these MSMQ apps with SQL Service Broker Queues (SSB). With ILM 2007 /MIIS 2003 SP 2 supporting SQL 2005 the use of SQL Service Broker Queues became much more accessible to ILM Developers.  
  
  
  
Here is an article comparing MSMQ with SQL Service Broker Queues  
  
[http://www.devx.com/dbzone/Article/34110](http://www.devx.com/dbzone/Article/34110)  
  
  
  
Here it is another discussion on the matter in an MSDN forum:  
  
[http://forums.microsoft.com/MSDN/ShowPost.aspx?PostID=661768&SiteID=1](http://forums.microsoft.com/MSDN/ShowPost.aspx?PostID=661768&SiteID=1)  
  
  
  
Here is an interesting blog post about working with both SQL Service Broker Queues (SSB) and  
  
Windows Workflow Foundation:  
  
[http://devhawk.net/2006/12/11/Transactions+In+Workflow+Foundationland.aspx](http://devhawk.net/2006/12/11/Transactions+In+Workflow+Foundationland.aspx)  
  
The DevHawk has many good insights into SSB.  
  
  
  
One huge advantage to me in dealing with SSB is that I can query a view just like a table to examine its current contents. SSB is also very easy to scale out.  
  
At DEC 2008 Craig Martin and Marshall Hamilton (both from OCG North America) spoke on the SSH MA (originally developed by Patrick Rempel from OCG Germany) which is being used to manage thousands of Unix servers (well together multiple instances of the MA are managing several thousand servers) through SSH connections and issuing he command line commands to create users etc.  
  
One problem they had to solve was what if one server is down during import? Regurgitate data for systems that are down which necesitates caching the data somewhere. Another problem I envision in such scenarios is that performance is probably an issue. Imagine a slightly different design.  
  
What if an intermediate database was used to hold the results from the servers. Importing data from the servers on separate schedules, then importing to ILM on yet another separate schedule. The requests to import could be popped into a queue for multiple processes to implement. For executing exports have the XMA pop the requests into a SSB queue and then have a process that pulls info from the queue. If performance on export becomes an issue it is child's play to scale out with SSB, add another process that pulls import request messages from the queue.  
  
Another use case for SSB is to replace anytime MSMQ has been used. Benefits: SSB can be clustered for failover, back up is as simple as backing up the database hosting the SSB queues.  
  
[For a Gentle Intro to SSB](http://www.develop.com/us/email/developments/developmentsfinal110707.htm)

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices