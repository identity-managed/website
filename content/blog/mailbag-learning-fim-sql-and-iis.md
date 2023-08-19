---
title: 'Mailbag: Learning FIM, SQL and IIS'
date: 2014-04-18T17:21:00.000-07:00
draft: false
url: /2014/04/mailbag-learning-fim-sql-and-iis.html
tags: 
- SQL
- FIM
- IIS
---

Recently, a reader reached out to me for advice on learning FIM, SQL and IIS. As well as guidance on setting up a lab (more advice on that part in a later post).  
  
First think for a moment about your best learning styles for technology. Do you need to read the concepts and architecture first and then do it? Do you need to watch a video and then read, and then do it? Do you need to try it and then go back and read? Do you need an instructor? Sometimes you have to learn through experimentation. In the early days of ILM 2 Beta there wasn't much info so we had to experiment. Brad Turner and I spent many days in a lab configuring and trying things out to see what was the best practice.  
  
Fortunately there are a fair amount of videos, articles, [virtual labs](http://technet.microsoft.com/en-us/virtuallabs/bb467605.aspx) and classes about all three subjects. In general I find the virtual labs to be a great way to get in and get some quick hands on lab knowledge without having to labor endlessly to setup your own lab. Not that you won't get something out of that experience. But sometimes you need to pickup tidbits or try something out before deciding you need to setup a more permanent lab to experiment with.  
  
FIM, SQL and IIS rely on Windows Server, Active Directory and Networking. It is surprising how many issues get resolved through knowledge of basic networking and its troubleshooting tools. Understand how client applications use DNS to find what they are looking for and SPNs to authenticate through Kerberos.  If you are shaky or want a refresher I encourage people to start with those topics.  
  
For FIM I would start with the [Ramp Up training.](http://technet.microsoft.com/en-us/ff793470.aspx) It provides you with video, lab manuals and the virtual labs. Of course I also recommend my book. There is also another FIM book by Kent Nordstrom. Beyond that here is a great list of resources: [http://social.technet.microsoft.com/wiki/contents/articles/399.forefront-identity-manager-resources.aspx#Learning\_FIM\_TwentyTen](http://social.technet.microsoft.com/wiki/contents/articles/399.forefront-identity-manager-resources.aspx#Learning_FIM_TwentyTen)  
  
SQL: this is more in the context of what you need to know about SQL to support FIM. Start with a presentation I gave a few years ago at The Experts Conference on [Care and Feeding of the databases](http://www.ilmbestpractices.com/files/RidetheChaosThroughProperCareAndFeeding.pptx)  
 as this gives you some perspective on what you need to SQL to support FIM. Configuring overall memory for SQL, TempDB configuration, Index management, Backups, Transaction Logs, Recovery Models. The last chapter of FIM Best Practices Volume 1 covers how to intelligently automate your SQL maintenance.  
  
If you want to start learning SQL queries try [http://www.ilmbestpractices.com/files/I\_Dream\_in\_SQL.zip](http://www.ilmbestpractices.com/files/I_Dream_in_SQL.zip)  or take the [Microsoft course](http://www.microsoft.com/learning/en-us/course.aspx?ID=10774A)  
  
IIS: Again this is in the context of what you need to know about IIS to support FIM.  
Overview of IIS 8 (Windows 8 and Windows Server 2012) [http://technet.microsoft.com/en-us/library/hh831725.aspx](http://technet.microsoft.com/en-us/library/hh831725.aspx)  
  
Overview of IIS 7 [http://technet.microsoft.com/en-us/library/cc753734(v=WS.10).aspx](http://technet.microsoft.com/en-us/library/cc753734(v=WS.10).aspx)  
  
Great [post comparing how IIS 6 through 8 deal with SSL](http://blogs.msdn.com/b/kaushal/archive/2013/05/27/difference-in-iis-6-iis-7-x-and-iis-8-with-regards-to-ssl.aspx).  
  
Intro to IIS 8 virtual lab [http://go.microsoft.com/?linkid=9838455](http://go.microsoft.com/?linkid=9838455)  
  
  
  

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices