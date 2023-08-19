---
title: 'Open Source: Review of Lithnet'
date: 2017-03-31T19:35:00.002-07:00
draft: false
url: /2017/03/open-source-review-of-lithnet.html
tags: 
- PowerShell
- OpenSource
- MIM
- FIM
- Review
---

Ryan Newington's [Lithnet](https://github.com/lithnet) consists of several items:  
  

1.  [miis-powershell](https://github.com/lithnet/miis-powershell)
2.  [resourcemanagement-powershell](https://github.com/lithnet/resourcemanagement-powershell)
3.  [resourcemanagement-webservice](https://github.com/lithnet/resourcemanagement-webservice)
4.  [googleapps-managementagent](https://github.com/lithnet/googleapps-managementagent)
5.  [acma](https://github.com/lithnet/acma)

1.  "Codeless business rules engine for FIM/MIM"

7.  [umare](https://github.com/lithnet/umare)

1.  "Codeless data transform engine for FIM/MIM"

  
I will only review the items I know  
  
**Managing Sync**  
[miis-powershell](https://github.com/lithnet/miis-powershell) is amazing it can almost everything you can do through the UI. For example, Clear-FullSyncWarning and it has a great wiki. Gotta have it!  
  

It wraps WMI calls, existing PowerShell modules, executables and sync client UI to interact with FIM/MIM Sync.

  

My WishList

Turn on and off Sync Rule Provisioning

  

Export Sync Server Config

  
**Managing Service**  
  
I know many people love Ryan's approach with [Lithnextresourcemanagement-powershell](https://github.com/lithnet/resourcemanagement-powershell) as it enables you to interact with the FIM/MIM Service in great ways. My big downside is that you just about have to learn a [new language, the Config Management XML](https://github.com/lithnet/resourcemanagement-powershell/wiki/Configuration-management) to use this most effectively. But when you do you can have every piece of FIM/MIM Service under source code control. Ike Ugochuku (recent MVP -- congrats!) has a [nice video intro](http://ike%20ugochuku/)   
  
So while I use Wim Beck's [IS4U-FIM-PowerShell](https://github.com/wim-beck/IS4U-FIM-Powershell) (Check out my [review of IS4U-FIM-PowerShell](http://blog.ilmbestpractices.com/2017/03/open-source-review-of-is4u-fim.html)) I can wholeheartedly concur with other's recommendations that this is worthwhile!  
  
**Simplifying the Service**  
The [Resourcemanagement-WebService](https://github.com/lithnet/resourcemanagement-webservice) is not something I have used but as one of the first beta users of the SOAP/WCF endpoint back in ILM 2 Beta 2 days I can really appreciate the notion of a simplified, Restful interface that returns JSON instead of bloated XML. Good work!  
  
The other pieces will have to wait for another time.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices