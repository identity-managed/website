---
title: 'Open Source: Review of FIM PowerShell Module'
date: 2017-03-31T18:52:00.005-07:00
draft: false
url: /2017/03/open-source-review-of-fim-powershell.html
tags: 
- PowerShell
- OpenSource
- MIM
- FIM
- Review
---

The [FIM PowerShell Module](http://fimpowershellmodule.codeplex.com/) (started by [Craig Martin](http://www.integrationtrench.com/) and now updated most frequently by [Brian Desmond](http://briandesmond.com/)) is a great set of commandlets that help you to automate Interactions with FIM Service and FIM Sync Service.  
  
**Managing Sync**  
This library is great for automating tests. This library and Ryan Newington's [Lithnet-Miis-PowerShell](https://github.com/lithnet/miis-powershell) (see [my review on LithNet](http://blog.ilmbestpractices.com/2017/03/open-source-review-of-lithnet.html)) are very complimentary. You can retrieve CS Objects, Run History, start an MA.  
I found that the most interesting Sync related Cmdlets are the  

*   Assert-CSAttribute, which you use to do automated test checking and
*   Create-ImportfileFromCSEntry which you can use to take a CSEntry and make a drop file as a way to fake connections to the connected system. So you can run an export and then confirming import

  

Other CmdLet's not covered by LithNet

*   Get-FimRegistryKey
*   Get-FimSyncPath

  

*   Get-ImportAttributeFlow
*   Get-ExportAttributeFlow
*   Join-ImportToExportAttributeFlow
*   Get-MetaverseSchema

  
For documenation purposes the Get- AttributeFlow commandlets are amazing. I can't believe I ever implemented FIM or MIM without them. You can use them to generate a view of the end to end flow of attributes.  
  
I felt cool when I got to apply some code from [Joe Zamora](http://blog.idmware.com/2013/03/one-small-addition-to-powershell-module.html) and a couple fixes of my own to solve these issues:  

[http://fimpowershellmodule.codeplex.com/workitem/1898](http://fimpowershellmodule.codeplex.com/workitem/1898)

[http://fimpowershellmodule.codeplex.com/workitem/2062](http://fimpowershellmodule.codeplex.com/workitem/2062)

  

  

[http://fimpowershellmodule.codeplex.com/workitem/2347](http://fimpowershellmodule.codeplex.com/workitem/2347)

Brian Desmond was kind enough to perform the commits. 

  
**Managing MIM Service**  
These PowerShell commandlets tend be very robust with lots of great error checking. They are great for creating objects in the FIM/MIM Service. They do lack commandlets for updating and deleting specific objects but that can still be handled with the New-FIMImportObject and New-FIMImportChange commandlets.  
  
I also found that while many commandlets have a $uri parameter that should allow you to call the cmdlets and affect a remote installation some of the underlying commandlets don't implement this consistently and expect a local instance of the Service.  
  
This library provides a great foundation upon which Wim Beck built [IS4U-FIM-PowerShell](https://github.com/wim-beck/IS4U-FIM-Powershell) (Check out my [review of IS4U-FIM-PowerShell](http://blog.ilmbestpractices.com/2017/03/open-source-review-of-is4u-fim.html)). I recommend that library (plus this one) or Ryan Newington's [Lithnextresourcemanagement-powershell](https://github.com/lithnet/resourcemanagement-powershell) ([see my review](http://blog.ilmbestpractices.com/2017/03/open-source-review-of-lithnet.html)).

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices