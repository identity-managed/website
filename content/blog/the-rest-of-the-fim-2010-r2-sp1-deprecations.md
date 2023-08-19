---
title: 'The rest of the FIM 2010 R2 SP1 Deprecations'
date: 2013-01-17T11:22:00.001-07:00
draft: false
url: /2013/01/the-rest-of-fim-2010-r2-sp1-deprecations.html
tags: 
- Forefront Identity Manager
- FIM 2010 R2
- FIM
---

Remember that these features are still here but will be removed in a future version (probably the next major release or the one after)

Feature

Impact

Unselect “allow nulls” for exported values

You need to be more careful to ensure that you aren't deleting values

Web Service configuration interface

You will no longer be able to send a request to the web service to update the mv-data or ma-data objects in order to configure the sync engine. The article says that we will be able to use PowerShell to configure the sync engine.

Running Connectors(MA) out of process

Can no longer run the MA out of process

Run Rules Extensions out of process

Can no longer run rules extensions out of process

Join on “Any” object type

Shouldn't be doing that anyway it makes your join search far less efficient.

“Do not recall attributes”

Yeah! I always hated this feature as I have seen many Metaverse attributes left in states where you can't update that attribute in the Metaverse -- especially if the contributing MA has been decommissioned

Exchange 5.5 Utils

Are you still provisioning to Exchange 5.5? Way past time to upgrade!

Configure partition display name

This really only applied to the old MIIS password change site that hasn't been part of the product since ILM 2007 shipped.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices