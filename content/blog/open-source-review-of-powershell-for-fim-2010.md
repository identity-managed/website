---
title: 'Open Source: Review of PowerShell for FIM 2010'
date: 2017-03-31T19:15:00.000-07:00
draft: false
url: /2017/03/open-source-review-of-powershell-for.html
tags: 
- PowerShell
- OpenSource
- MIM
- FIM
- Review
---

[PowerShell for FIM 2010](http://fim.codeplex.com/) by Adam Weigert consists of three parts but I further break the last into two:  
  

1.  Management Agent(MA)  and MetaVerse (MV) Extensions that let you run PowerShell scripts as your extensions
2.  A Workflow Activity
3.  A PowerShell module

1.  Managing Sync
2.  Managing Service

  
**Management Agent(MA)  and MetaVerse (MV) Extensions**  
The work done to enable you to write PowerShell scripts to be MA and MV extensions is crazy brilliant. However, I suspect (I haven't tested) that large installations should shy away from this as compiled C# and VB.NET code tends to run orders of magnitude faster than PowerShell scripts. Perhaps someone else knows a way to make it more comparable in performance. I can see some smaller shops taking advantage of this as they don't need to worry about performance in the Sync Engine  
  
**Workflow Activity**  
The workflow activity (see [my review of a bunch of open source Workflow activities](http://blog.ilmbestpractices.com/2016/12/christmastime-fimmim-open-source-wf.html)) was good in its time but like most has been surpassed by the excellent MIMWAL.  
  
**Managing Sync**  
Similar to the [FIM PowerShell Module](http://fimpowershellmodule.codeplex.com/) you can Get an MA's status, start it, and get the run history. It does go beyond that by allowing you to Clear the RunHistory, and Stop an MA. However all of these features are covered in  Ryan Newington's [Lithnet-Miis-PowerShell](https://github.com/lithnet/miis-powershell) (see [my review on LithNet](http://blog.ilmbestpractices.com/2017/03/open-source-review-of-lithnet.html)). This library is good but I recommend using the [FIM PowerShell Module](http://fimpowershellmodule.codeplex.com/) and [Lithnet-Miis-PowerShell](https://github.com/lithnet/miis-powershell)   
**Managing Service**  

This library has a nice simple model for creating, updating and deleting FIM/MIM resources. It is easier to use than [FIM 2010 PowerShell Cmdlets](http://fimpscmdlets.codeplex.com/). However, the simple model doesn't add lots of intelligence to help you with creating and managing the various resource types.

  

This may indeed be the approach you want.  
  
I prefer  [IS4U-FIM-PowerShell](https://github.com/wim-beck/IS4U-FIM-Powershell) (Check out my [review of IS4U-FIM-PowerShell](http://blog.ilmbestpractices.com/2017/03/open-source-review-of-is4u-fim.html)).   
  
I can see how others would prefer [Lithnext resourcemanagement-powershell](https://github.com/lithnet/resourcemanagement-powershell) ([see my review](http://blog.ilmbestpractices.com/2017/03/open-source-review-of-lithnet.html)).

  

Here is an incomplete example from my notes:

New\-FIMResource \-ObjectType 'ManagementPolicyRule' \-Set @{  
  DisplayName \= 'Users Can Edit Preferred Names with Approval';

Description ='Users can edit preferred names with their managers approval which are then used to calculate their new displayname';

PrincipalSetID = $Principalset; GrantRight= $True; ManagementPolicyRuleType= ''; AuthwfID= $AuthWFID; ActionWfID $ActionWfID; Disabled $false;

} \-Add @{

ActionParameter\= @('PreferredLastName', 'PreferredFirstName')

; ActionType = @('','')} | Set\-FIMResource

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices