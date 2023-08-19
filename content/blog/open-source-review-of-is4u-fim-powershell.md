---
title: 'Open Source: Review of IS4U-FIM-PowerShell'
date: 2017-03-31T19:52:00.001-07:00
draft: false
url: /2017/03/open-source-review-of-is4u-fim.html
tags: 
- PowerShell
- OpenSource
- MIM
- FIM
- Review
---

Wim Beck's [IS4U-FIM-PowerShell](https://github.com/wim-beck/IS4U-FIM-Powershell) is a great example of open source, in that he has built on top of the  [FIM PowerShell Module](http://fimpowershellmodule.codeplex.com/) ([see my review](http://blog.ilmbestpractices.com/2017/03/open-source-review-of-fim-powershell.html)). This is what Open Source is about, building upon each other's contributions to make great stuff!  
  
When I looked at it in Dec 2016 I almost dismissed it since it lacked a wiki, but since then Wim has added a lot of pages. They still lack examples, I plan on pitching in to help out with that by adding some examples to my fork and then asking Wim to pull it in.  
  
Some of the commandlets don't do a good job of robust validation of parameters. Another area that could use some community involvement.  
  
For me the approach of having commandlets focused around different object types allows for a natural and better validation of the data you need to create, update and delete objects in the FIM/MIM service.  
  
One great example of building on things is the New-ObjectTypeConfiguration commandlet which (creates object type in the schema, the attributes, the bindings, an MPR for permissions, a search scope, a navbar element, and updates the sync filter). Awesome!  
  
I also love the RCDC commandlets. Test-RCDCConfiguration just does a simple test against the XSD which you can setup Visual Studio to do for you, but this allows you to test it programatically after make programatic changes to an RCDC object before you upload it. I did feel the need to extend this and added a function to backup the RCDC and another to backup all of the RCDC's. I will add those to my fork when I get the chance.  
  
I use this module and it saves me a lot of time. I am glad to see Wim continuing to work on it, smoothing out the rough edges.  
  
I can see how some might prefer the config file approach of Ryan Newington's [Lithnextresourcemanagement-powershell](https://github.com/lithnet/resourcemanagement-powershell) ([see my review](http://blog.ilmbestpractices.com/2017/03/open-source-review-of-lithnet.html)), which I also recommend.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices