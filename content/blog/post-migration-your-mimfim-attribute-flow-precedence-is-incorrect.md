---
title: 'Post Migration Your MIM/FIM Attribute Flow Precedence is Incorrect'
date: 2016-10-17T23:53:00.004-07:00
draft: false
url: /2016/10/post-migration-your-mimfim-attribute.html
tags: 
- Forefront Identity Manager
- Microsoft Identity Manager
- MIM
- FIM
---

Have you ever found out that attribute flow precedence is messed up, wrong or otherwise in error just after you followed [the steps to migrate your MIM/FIM configuration](https://technet.microsoft.com/en-us/library/ff400277(v=ws.10).aspx) from Dev to Prod or vice-versa? Well I am finally blogging about a discovery I made. The list of steps (reproduced below from the above link) are incomplete:  

1.  Back up the pilot and production environments by using the Backup and Restore procedures.  
    
2.  Export the FIM Service schema configuration.  
    
3.  Export the FIM Synchronization Service configuration.  
    
4.  Export the FIM Service policy and FIM Synchronization Service configuration resources.  
    
5.  Install the FIM Synchronization Service and the FIM Service in the production environment.  
    
6.  Enable the maintenance mode in the production environment.  
    
7.  Import the FIM Service schema configuration.  
    
8.  Import the FIM Synchronization service configuration.  
    
9.  Install the custom DLLs necessary for custom workflows.  
    
10.  Import the FIM Service policy and FIM Synchronization Service configuration.  
    
11.  Disable maintenance mode in the production environment.

After Step 10 "Import the FIM Service Policy" your attribute flow precedence will get messed up if you had changes to inbound sync rules that write to the same attributes as any import attribute flows defined in the management agents.  
  
**Here is why**: After step 10 you have imported the sync rules into the FIM Service and Portal but until you run an import on the FIM MA those sync rules and their attribute flows are not yet in the sync engine. Once you run the FIM MA import then you have those flows but the precedence may not match the precedence in the source environment.  
  
**Solution**: After step 10 Run a Delta Import and Delta Sync on the FIM MA. Then reimport the FIM Sync configuration (Step 8).  
  
**Why this works**: This gets the sync rules and their attributes flows into the Sync engine and then reapplies the attribute flow precedence from the source environment.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices