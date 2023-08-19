---
title: 'Best Practices ILM 2007 Coding Conventions and Habits'
date: 2009-06-22T15:31:00.001-07:00
draft: false
url: /2009/06/best-practices-ilm-2007-coding.html
tags: 
- ILM
---

In response to question in the MMSUG yahoo group I thought I would post the following:

**Naming conventions for MV objects and attributes.**

Most CS objects and attributes come to us with names -- the exception being when we are writing our own views in SQL or Oracle

There are many object types and attributes pre-defined in the metaverse if you use those no need to rename most of them seem to come from the required and suggested  attributes for either an X.500 Directory or LDAP Directory.

For new objects it depends on how you want to process things. If you need to take some code based actions that are identical for similar but different object types then using a prefix or suffix can help. I have seen some very complex GALSync scenarios implemented that way, div-Person, div2-Person, div3-Person, div-DL, Div2-DL, Div3-DL, div-Contact, div2-Contact, div3-Contact.  Then in provisioning code you can match on patterns to make decisions.

For Attributes some like to create them with a prefix with the client name. I generally like to match my attributes to the names from LDAP.

**Naming conventions for coded attribute flows (AF).**

In the 2731 class the instructions have you replacing the generated name User.samAccountName -> Person.sAMAccountName with something more like SamAccountName.

The benefit of the generated names is that they are pretty much unique and human readable although they are long. These days I tend to leave the default names.

  
**Ways to make extensions for AF more adjustable without re-coding.**

I have seen one developer use the flow rule names as a language to processor module to handle 90% of his string manipulation. That certainly cut down on the need for re-coding.

That may have been an extreme example but it shows you what is possible.

Another tactic is to preprocess Attribute flow by performing the transformations in a SQL view -- it is much faster, but you can only use information available from that database. If you need to change it you won't need to change the MA Extension code. This is my preferred approach.

  
**Ways to make provisioning code more adjustable without re-coding.**

Make use of XML config files to store things like Exchange Mailbox stores to use, and then read them in during the initialize method (called once when the dll is loaded, since the dll's stay in cache for 5 min after use this won't necessarily be every run) of the Provisioning dll, and then make use of them during the provision method (called once per connected cs object being synchronized). Don't load an xml config file in the provisioning method unless you are looking for a way to slow down performance.

  
**Favorite ways to make the status for any particular object easy to understand for people who don't know ILM/AD, etc.**

We like to use reports and give the reports and their columns good descriptive names like ILM Disconnectors. Uh I mean AD Objects (Users, Groups OUs etc) that don't have matches in the other systems (like HR).

In the reports on connected objects using the binary functions in SQL to translate

For info on reports see Brad Turner's blog on the [community reporting pack](http://www.identitychaos.com/2007/05/update-miis-reporting-pack-announced.html) that he created (I helped but only on one report).

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices