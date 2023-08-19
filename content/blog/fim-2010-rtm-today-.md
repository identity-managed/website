---
title: 'FIM 2010 RTM Today!'
date: 2010-03-02T13:03:00.001-07:00
draft: false
url: /2010/03/fim-2010-rtm-today.html
tags: 
- Forefront Identity Manager
- ILM
- Identity Management
- FIM
---

Today, March 2, at the RSA conference Microsoft announced the release to manufacturing of Forefront Identity Manager 2010 (FIM, formerly codenamed ILM “2”) with General Availability starting next month.

Download the eval here:

[Microsoft® Forefront™ Identity Manager 2010 Evaluation Version](http://www.microsoft.com/downloads/details.aspx?displaylang=en&FamilyID=22731a2a-5b0f-4c6b-846a-e53588117981)

Yeah!

FIM gives us capabilities for User provisioning (and deprovisioning), Group management, Self-Service Password Reset, Password Synchronization, Workflows with Approvals, User profile self-service management, and accomplishing these items through Declarative Provisioning. Yet FIM retains an incredible set of extensibility points, allows customization of the Portal, schema of the objects, managing new systems, custom workflows, custom clients to the FIM web service.

According to the release notes there are some nice new enhancements:

> You can now have explicit members in a set which has a defined filter (so sets can have dynamic members based on the filter and explicitly added members).
> 
> Password Reset now accepts the user principal name (UPN) as well as the fully qualified domain name (FQDN) when specifying user credentials  

In addition to the enhancements found in [RC 1](http://www.ilmbestpractices.com/blog/2009/10/fim-rc-1-is-here-whats-new.html) and its [update 1](http://www.ilmbestpractices.com/blog/2009/11/update-to-fim-rc1.html), [update 2](http://support.microsoft.com/KB/977312) and [update 3](http://www.ilmbestpractices.com/blog/2010/02/final-update-for-fim-rc1-released.html) ([Brad’s take](http://www.identitychaos.com/2010/02/fim2010-rc13-update-3-good-and-bad.html) on update 3):

> Adds support for SQL Server Failover Clusters for High Availability
> 
> New type of MPR (Set based Transition vs. Request based)
> 
> · Adds support for taking database backups without stopping the FIM Service.
> 
> · New Supported Platforms for FIM Certificate Management
> 
> · Windows Server 2008 R2
> 
> · Windows Server Datacenter edition
> 
> · Added support for Exchange 2010 for the following scenarios:
> 
> · FIM Synchronization Service support for Active Directory Management Agent and GAL Management Agent
> 
> · The FIM Service sending and receiving mail
> 
> · Outlook 2007 on Exchange 2010 sending approvals and group membership requests
> 
> · You can now copy and paste a vertical list from Excel to the Resource Picker input box. This is especially useful for doing bulk Adds.

> · The UOC text box now lets you check uniqueness using a custom XPATH statement that you provide.

> The FIMMA will now store error messages with the operation during export. You do not have to look in the FIMService event log anymore to see the errors.

> You can now have several MAs that are responsible for deleting a resource, which solves a common problem where custom code still was needed for declarative provisioning.

· Added two new Declarative provisioning functions:

> · Null – This Synchronization Rule should not contribute a value to support not flowing values to disabled accounts.

> · ReplaceString – Find and replace a substring in another string

Added support for Exchange 14 mailbox provisioning

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices