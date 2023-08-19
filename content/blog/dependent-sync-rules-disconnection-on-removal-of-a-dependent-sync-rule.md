---
title: 'Dependent Sync Rules – Disconnection on removal of a dependent Sync Rule'
date: 2010-06-29T14:32:00.001-07:00
draft: false
url: /2010/06/dependent-sync-rules-disconnection-on.html
tags: 
- Forefront Identity Manager
- FIM
---

Recently, I discovered that under certain conditions the removal of a dependent sync rule could cause the disconnection of objects in AD or other connected data sources. So I had to investigate the inner workings of dependent Sync Rules to uncover this mystery and fix it.

FIM allows us to create dependent Sync Rules. First let me explain the what and then a little why. Then allow me to explain a bug that I discovered and how to work around it.

A Dependent Sync Rule is an outbound sync rule, or and inbound and outbound sync rule (with only the outbound side working) that depends on and inherits (at the time of creation) from its parent or base sync rule.

A base Sync Rule is one that doesn’t depend on any other sync rule.

A dependent sync rule can depend on another dependent sync rule.

A dependent sync rule cannot be applied to a resource until its parent sync rule has been applied

When you create a sync rule as a dependent sync rule it inherits a number of attributes from the parent

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/DependentSyncRulesDisconnectiononremoval_CC43/image_thumb.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/DependentSyncRulesDisconnectiononremoval_CC43/image.png)

Let’s break it down:

> The resource Type is obviously sync rule

> Create External System Resource, Create FIM Resource, and Disconnect External System Resource are all set to false because this is a dependent sync rule. Back in RC 1 Disconnect External System Resource inherited the value of the parent which leads to odd behavior I will describe further on in the post. The attributes and their corresponding actions are the province of base sync rules.

> Data Flow Direction (1 for outbound or 2 for in and out), External System, External System Resource Type, FIM Resource Type, and Relationship criteria are inherited from the parent.

> Workflow Parameters and persistent flow can be set as well as the DisplayName and the Description. Initial flow can’t be set as that is also the province of base sync rules.

Why implement dependent sync rules? Flow additional attributes in a situational fashion but only if some base sync rule is already applied.

**One danger can occur**. If you create a base sync rule, set the Disconnect External System Resource to true and then change it to a dependent sync rule, the disconnect remains true and you have no way in the UI to change it since the scoping and relationship tabs are hidden for dependent sync rules. So the bug is either that you can’t change it in the UI or that the UI or service should be changing it to false if the rule becomes dependent.

If this setting is set to true then it might disconnect the resource when the dependent sync rule is removed.

This can also happen if you load a sync rule through the web service as dependent and set the Disconnect External System Resource to true.

How did it get this way? Well if you were an RDP or TAP customer and you had RC 1 and then upgraded your FIM Service database it could be that way. Or if you export the FIM sync rule from one system and it was like that and then went to another it would load in with it set to true

How to find out if you have this?

Assuming you have already imported and sync’d from the FIM MA then In the Sync Service Manager, go to metaverse search. Search for Sync rules. Search for those with the DisconnectConnectedSystemObject set to true and dependency is present. If anything turns up then you have this issue.

To solve it you can use the UI or this  PowerShell script against the web service.

To use the UI you open the dependent sync rule change it to not have a dependency and then change it back to depend on the one that it had before. That seems to tell the UI to set Disconnect External System Resource to false

Initially your dependent sync rule looks like this:

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/DependentSyncRulesDisconnectiononremoval_CC43/image_thumb_3.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/DependentSyncRulesDisconnectiononremoval_CC43/image_3.png)

So change it to look like this (but don’t click OK and submit – not yet anyway)

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/DependentSyncRulesDisconnectiononremoval_CC43/image_thumb_4.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/DependentSyncRulesDisconnectiononremoval_CC43/image_4.png)

Then change it back

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/DependentSyncRulesDisconnectiononremoval_CC43/image_thumb_3.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/DependentSyncRulesDisconnectiononremoval_CC43/image_3.png)

Then click OK and you should see this and nothing else getting changed

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/DependentSyncRulesDisconnectiononremoval_CC43/image_thumb_5.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/DependentSyncRulesDisconnectiononremoval_CC43/image_5.png)

Then click Submit.

Or use PowerShell on your next import and sync from FIM your sync rule will be fixed.

. C:\\FIMTasks\\FIMHelper\\FIMPowerShell.ps1

\# includes the helper functions from: [http://technet.microsoft.com/en-us/library/ff720152(WS.10).aspx](http://technet.microsoft.com/en-us/library/ff720152(WS.10).aspx)

\# and the GenerateFilter from [http://technet.microsoft.com/en-us/library/ff720142(WS.10).aspx](http://technet.microsoft.com/en-us/library/ff720142(WS.10).aspx)

\# and GetAttributeValueFromResource from [http://technet.microsoft.com/en-us/library/ff720158(WS.10).aspx](http://technet.microsoft.com/en-us/library/ff720158(WS.10).aspx)

\# take the above helper functions and create a file called FIMPowerShell.ps1 and put them in it

\# Purpose of this script is to Identify sync rules with dependencies

\# where the DisconnectConnectedSystemObject=true and set it to false

\# step 1 find Sync rules with dependencies and DisconnectConnectedSystemObject=true

\# step 2 Modify the DisconnectConnectedSystemObject=false for each of these

\# step 3 commit to FIM

function QueryResourceOnlyBase

{

PARAM($Filter, $Uri = $DefaultUri)

END

{

$resources = Export-FIMConfig -CustomConfig $Filter -Uri $Uri -OnlyBaseResources

$resources

}

}

\# step 1 find Sync rules with dependencies and DisconnectConnectedSystemObject=true

$uri = "[http://localhost:5725/ResourceManagementService](http://localhost:5725/ResourceManagementService)"

$exportedSyncRules = QueryResourceOnlyBase -Filter "/SynchronizationRule\[DisconnectConnectedSystemObject=true

and Dependency = /SynchronizationRule \]" -Uri $Uri

Write-Host ("The script has exported " + $exportedSyncRules.Count + " sync rules based on the filter: " + $query)

\# step 2 Modify the DisconnectConnectedSystemObject=false for each of these

$importList = @()

foreach ($syncRule in $exportedSyncRules)

{

$importObject = ModifyImportObject $syncRule.ResourceManagementObject.ObjectIdentifier "SynchronizationRule"

SetSingleValue $importObject "DisconnectConnectedSystemObject" "false" 1

$importList += $importObject

}

\# step 3 commit to FIM

if ($importList.Count -gt 0 )

{

$undoneChanges = $importList | Import-FIMConfig -Uri $Uri

\# Use ConvertFrom-FIMResource cmdlet to convert contents of $undoneChanges to the file "undone.xml".

if ($undoneChanges.Count -gt 0)

{

Write-Host "There are " + $undoneChanges.Count + " sync rules that failed to update"

Write-Host "The undone imports are written to undone.xml"

$undoneChanges | ConvertFrom-FIMResource -file undone.xml

}

Write-Host "Import complete"

}

else

{

Write-Host "Nothing to import"

}

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices