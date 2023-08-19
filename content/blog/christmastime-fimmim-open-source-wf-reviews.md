---
title: 'Christmastime FIM/MIM Open Source WF Reviews'
date: 2016-12-24T13:39:00.002-07:00
draft: false
url: /2016/12/christmastime-fimmim-open-source-wf.html
tags: 
- Forefront Identity Manager
- FIM 2010 R2
- Microsoft Identity Manager
- Workflow
- MIM
- FIM
---

Over the years since FIM was first beta'd as ILM2 we have seen some cool workflows be released to open source. This is my review of the workflows I can find that are open source. First let me salute everyone who has contributed to the FIM and MIM community with these big undertakings. That said I am trying to give guidance to my readers as to what is the most useful in various situations and so I will make specific recommendations.  
  
So what's under the tree for Open Source Workflows?  
  

Project Name

Developer(s)

Link

Last Activity

Conclusion

MIMWAL

 JefTek, Nilish Ghodekar

[https://github.com/Microsoft/MIMWAL](https://github.com/Microsoft/MIMWAL)

Oct 2016

Gotta have it -- this recent addition to the FIM/MIM world is great! But must have FIM 2010 R2 (4.1.3496) or later

FIM Powershell Workflow Activity

Craig Martin, Brian Desmond, Henrik Nilsson, James Booth

[http://fimpowershellwf.codeplex.com/](http://fimpowershellwf.codeplex.com/)

Sept 2013

Superseded (but if you still haven't upgraded to FIM R2) -- Great when it first came out but now use MIM WAL instead

PowerShell for FIM 2010

WorkFlowActivity (other features reviewed elsewhere)

Adam Weigert

[http://fim.codeplex.com/](http://fim.codeplex.com/)

May 2014

Superseded -- Also nice when it first came out but now use MIM WAL instead

FIM 2010 Granfeldt Workflow Activity Library

Soren Granfeldt

[https://fimactivitylibrary.codeplex.com/](https://fimactivitylibrary.codeplex.com/)

Jan 2013

Maybe -- If MIMWAL Run PowerShell Script activity can't get it done or you already have C# code then use this

The Last FIM Workflow You Will Ever Need

Rebecca Croft

[http://fimwf.codeplex.com/](http://fimwf.codeplex.com/)

Feb 2013

Maybe -- If MIMWAL Run PowerShell Script activity can't get it done or you already have C# or VB.NET code then use this

FIM Workflow Library

Dave Nesbitt

[https://fimworkflowlibrary.codeplex.com/](https://fimworkflowlibrary.codeplex.com/)

June 2014

Possible -- If you are storing all of the accountNames or MailNickNames in SQL then take a look at this

ILM 2 RC0 Ensynch Custom Workflow Activity Libary

Joe Zamora

[https://ilm2rc0enswf.codeplex.com/](https://ilm2rc0enswf.codeplex.com/)

April 2009

Hidden nugget -- While this is more of a sample and the UpdateAttributeActivity has been superseded by MIMWAL (and others), the OwnerRollup Activity has value if you need to find a new owner to a group, service account when the existing owner is termed. Ditto for managing contractors

  
Details:  
  
MIMWAL:  

WF Building Block Activities (with conditional execution, iteration, Rich Functions, UI framework for creating new WF activities

  

Add Delay

Create Resource

Delete Resources

Generate Unique Value

Request Approval

Run PowerShell Script

Send Email Notification

  

Generate Unique Value

Can check FIM and LDAP for conflicts

Run PowerShell Script

Conditional execution

User

User Password

Impersonate

Load user profile

Log on type (batch job, svc)

Script Location (use an outside file or embedded in WF)

Inputs

Return

Send Email Notification

Can get Email Template from Xpath or Lookup

Addresses can come from Filter Search as well as lookup or email addresses

Can supress notification failure

Update Resources

Verify Request

  

  

FIM Powershell Workflow Activity

Run PowerShell from  Workflows

It has one property -- ScriptPath

Can access Workflow info such as RequestID, TargetID, ActorID, WorkflowDefinitionID, WorkflowDictionary

Decent docs

  

  

PowerShell for FIM 2010 WorkFlowActivity

Run PowerShell from FIM/MIM Workflows

Allows you to run as Requestor or as FIMService

  

Can access Workflow info such as RequestID, TargetID, ActorID, WorkflowDefinitionID, WorkflowDictionary

This module also can help manage FIM Service and FIM Sync and you can implement rules extensions and ECMA using PowerShell scripts

  

FIM 2010 Granfeldt Workflow Activity Library

WF Activities

Run C# code -- interact with WF Data or FIM Service

Reference libraries

Parameters

Specify your destination

Lookups

Create Object

Delete Object

Copy Values

  

Good solid library for customizing

  

The Last FIM Workflow You Will Ever Need

Let's you run VB.Net or C# code

Pick your Language, NameSpaces to use, and additional libraries to load, pick your Actor, Pass in parameters you need, specify a return type, and the destination attribute

  

  

Good solid library for customizing and allows you to choose between VB.Net and C#

  

FIM Workflow Library

Make Account Name -- pulls from SQL table

Make Email Alias

Set Entitlements

Docs very limited

Interesting that it pulls from SQL

  

ILM 2 RC0 Ensynch Custom Workflow Activity Library

UpdateAttributeActivity - An interim solution to the Function Evaluator limitations.

  

OwnerRollupActivity - Walk the manager chain to find a suitable owner.

One of the first Custom workflow activity libraries for FIM. Owner Rollup Activity is interesting as it allows you to find a new suitable owner for a Group or service account when the existing owner is terminated.

  
Disclaimer: some of these have been created by friends of mine and even by an employee. I have tried to review these purely from the view point of utility.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices