---
title: 'SQL 2008: Processor or Server/CAL'
date: 2008-08-16T12:57:00.001-07:00
draft: false
url: /2008/08/sql-2008-processor-or-servercal.html
tags: 
- ILM
- SQL Server Service Broker
- SQL Server
- SSB
---

Congrats to the SQL Server team for shipping 2008. It looks like a great product. Congrats as well for keeping the licensing costs the same and adding a new option with the web edition.

One question that many still have in mind is how to license SQL server. Processor licensing allows unlimited users and devices, whereas a server license allows unlimited users or devices as long as they have a CAL. Server CAL can be much cheaper than Processor license or it can become much more expensive.

Many ILM customers also have this question, and while the product team pushes you to processor licenses and says that if you want to go Server/CAL you need 1 CAL for each user that will connect directly to the SQL server (in case it does other stuff, or your ILM admins like to run unsupported queries under the hood) for each Management agent (how in the world did 1 device -- the ILM server -- become multiple devices and need many CALs? -- Maybe under some sort of multiplexing scenario since the data is getting pushed to other places) each situation will be different.

So I have developed a formula and a table to help you figure this out

Per Processor Licensing Costs =  
Cost Per Processor \* # of Servers \* Avg CPUs per Server

Server + CAL Licensing Cost =  
Cost Per Server \* # of Servers + Cost Per CAL \* # of CALs

Break Even Formula  
\# of CALs = (Cost Per Processor \* Avg CPU per Server - Cost Per Server) \* # of Servers/Cost Per CAL

As you can see the break even point between Server/CAL and Processor comes down to a ratio between CALs divded by the number of servers vs Processors (not cores, but physical packages) divded by the number of Servers. (Remember that one CAL allows one user or device to access an unlimited number of licensed servers -- you don't have to buy a CAL for each server you want to access. See [http://download.microsoft.com/download/2/d/f/2df66c0c-fff2-4f2e-b739-bf4581cee533/SQLServer%202008CompareEnterpriseStandard.pdf](http://download.microsoft.com/download/2/d/f/2df66c0c-fff2-4f2e-b739-bf4581cee533/SQLServer%202008CompareEnterpriseStandard.pdf "http://download.microsoft.com/download/2/d/f/2df66c0c-fff2-4f2e-b739-bf4581cee533/SQLServer%202008CompareEnterpriseStandard.pdf"))

[Using the sample licensing costs from Microsoft's site](http://www.microsoft.com/sqlserver/2008/en/us/pricing.aspx)

Edition

Workgroup\*

Standard

Enterprise

Per Processor

 $         3,700

 $       5,737

 $     23,911

Per Server

 $            730

 $         885

 $       8,487

Per CAL

 $            146

 $         162

 $          162

Using these sample numbers (and your costs maybe different)

**Break Even Points in terms of CALs per Server vs CPU/Server**

**Workgroup**

**Standard**

**Enterprise**

**CPUs/Server**

**CALs/Server**

**CALs/Server**

**CALs/Server**

1

                 25

              30

              95

2

                 51

              65

            243

4

 

            136

            538

6

 

 

            833

8

 

 

          1,128

10

 

 

          1,424

12

 

 

          1,719

14

 

 

          2,014

16

 

 

          2,309

18

 

 

          2,604

20

 

 

          2,900

32

 

 

          4,671

64

 

 

          9,394

10 SQL Enterprise Edition servers with an average of 2 quad core processors (that is still just two processors for licensing purposes) and I have less than 2430 (243x10) devices or users to license and am likely to maintain these ratios than Server/CAL should be cheaper than processor licensing. 20 processor licenses at $478,220 and 10 server licenses $84,870 plus $393,350 cost the same. Hiring more people and/or acquiring more devices might tip the balance, but acquiring more SQL servers or adding processors to existing boxes could counter that.

As you can see this is really an enterprise wide decision how will I license SQL servers for my organization.

What to do about users coming in from the web, well you can use processor licensing for those SQL servers or you could go with the web edition for $15 per processor per month. What about data on internal servers? Replicate it to the web edition server! SQL to SQL communication does not require a CAL.

Remember that ["SQL Server 2008 Web may be used only to support public and Internet-accessible Web pages, sites, applications, and services."](http://download.microsoft.com/download/2/7/6/27637d1d-337a-4d0a-b1d4-3f46c46d9513/SQL%20Server%202008%20Web%20datasheet.pdf)

In terms of features it is comparable to Workgroup edition, so none of the high availability features like clustering or mirroring are supported, only log shipping. There are several minor differences in the [functionality of Web vs Workgroup](http://msdn.microsoft.com/en-us/library/cc645993.aspx)

No ad hoc reporting through report builder, in service broker it can only be a client and its development tools come from SQL Express Management studio.

[http://msdn.microsoft.com/en-us/library/cc645993.aspx](http://msdn.microsoft.com/en-us/library/cc645993.aspx "http://msdn.microsoft.com/en-us/library/cc645993.aspx")

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices