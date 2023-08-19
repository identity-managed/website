---
title: 'FIM RC 1 is here – what’s new?'
date: 2009-10-04T22:46:00.001-07:00
draft: false
url: /2009/10/fim-rc-1-is-here-whats-new.html
tags: 
- Forefront Identity Manager
- FIM
---

FIM RC 1 is here.  Microsoft released it on Sept 30th which is the end of Q3 of 2009 which means the ILM/FIM team at Microsoft met their stated deadline announced back in March.

Here is the download:

[http://technet.microsoft.com/en-us/evalcenter/cc872861.aspx](http://technet.microsoft.com/en-us/evalcenter/cc872861.aspx "http://technet.microsoft.com/en-us/evalcenter/cc872861.aspx")

What’s new:

Gil Kirkpatrick has a nice post about the differences in the data structure:

[Auditing FIM 2010 RC1](http://www.gilkirkpatrick.com/Blog/post/2009/09/02/Auditing-FIM-2010-RC1.aspx "Auditing FIM 2010 RC1")

Darryl Russi a Sr. Test Lead at Microsoft has started blogging about FIM RC 1 performance:

[http://blogs.msdn.com/darrylru/archive/2009/10/01/fim-2010-performance-testing-introduction.aspx](http://blogs.msdn.com/darrylru/archive/2009/10/01/fim-2010-performance-testing-introduction.aspx "http://blogs.msdn.com/darrylru/archive/2009/10/01/fim-2010-performance-testing-introduction.aspx")

Microsoft has also included some pretty good documentation (available for independent download through the Microsoft connect site

[http://connect.microsoft.com/directory/](http://connect.microsoft.com/directory/ "http://connect.microsoft.com/directory/")

Search for

Forefront Identity Manager 2010 (FIM 2010) Beta

Pay careful attention to the Release Notes.
-------------------------------------------

One big thing I noticed, that I have been seeing with RC 0 and was hoping would be fixed with RC 1 was getting a “no-start-full-import-required” error during a delta import, however the release notes for RC 1 state:

> ###### Do not use delta-import with FIM MA
> 
> · In this release, always run a full import when synchronizing the FIM MA. Running a delta-import may result in a no-start-full-import-required error in some scenarios.

There are also several FIM schema changes you can make that make it impossible to restart the service and require a reinstall so keep an eye out for those: “\[creating\] a multi-valued Boolean attribute”, “\[creating\] custom attributes or resource types with duplicate names”,  or “\[creating\] a binding that uses the same resource type and attribute combination as another binding.” These last two are possible through the web service.

Password Reset
--------------

A nice thing is that the standard Password Reset workflows and MPRs are pre-created for you. I guess some people saw my Visio diagram of the fairly complex Password Reset process and heard the woes of everyone that tried to set it up. Kudos! This is possible because Management Policy Rules (MPRs) can be enabled and disabled!

Name Changes
------------

Among other things is a documentation road map listing all of the documents available for IT Pros and an Identity Terminology guide. Defines almost everything including XAML, but they forgot XOML. They have changed some names but don’t mention the old name so here is my best attempt:

Old Name

New Name

Comment

ILM 2

FIM

When Microsoft announced the name change back in April they said “ForeFront means business ready security.” I don’t know how you feel about Forefront Client Security but everything from Antigen, to ISA, to IAG, to ILM has been rebranded to Forefront. Does this mean that ForeFront Stirling is going to monitor FIM? I don’t know.

Object Visualization Configuration (OVC)

resource control display configuration (RCDC)

Same thing, new name, same limitations:  “you cannot write a customized function (Handler)” (Introduction to

resource control display configurations)

Although the documentation is much clearer on those limitations, and greatly expands on other topics as well.

CLM

FIM CM

FIM Certificate Management

Install Guide
-------------

The install guide looks fairly complete, just change any references to Enterprise Manager to mean Management Studio. When SQL 2005 came out I kept calling it Enterprise Management Studio (yes I would stutter on Manager-ment).

A big thing to note is this:

> ###### Assign enough space for the database
> 
> The FIM Service database will not autogrow even if those settings are enabled by default by SQL Server. You should expand the Data and Log files to be able to hold all data needed.

Wow! No autogrowth! I saw that happen with RC 0 but couldn’t believe it.

It also includes documentation on the parameters for unattended install. As you know from prior post my team and I prefer unattended installs.

Migrating from Test to Prod
---------------------------

There is a document called “Introduction to the Configuration Migration Tool”

> This document describes how to migrate a FIM 2010 configuration from a test environment to a production environment.

Yeah! We so needed this tool! Powershell! Sweet!

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices