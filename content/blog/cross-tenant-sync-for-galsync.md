---
title: Cross Tenant Sync for GalSync?
description: Can Microsoft's Entra ID Cross Tenant Sync accomplish GalSync?
tags:
  - GalSync;EntraID;CrossTenantSync
date: 2025-04-04T22:18:27.442Z
banner: /img/galsync_business.png
---
Microsoft Entra ID's Cross Tenant Sync can sync users from one tenant to another.  They will sync as External Members or External Guests. In Exchange Admin they will show as MailUsers.

Just be sure that showInAddressList is synced to be true or better yet carries over the showInAddressList from your source tenant.

**GalSync done! Yeah!**

Wait a minute! What about Groups? What about contacts? What about internal guests?

**N﻿O! They are not supported**

![](/img/crosstenantsync_groups-not-supports.png)

### O﻿ther limitations:

C﻿ross Tenant Sync will not sync photos, custom security attributes, user attributes, but it can sync Directory Extensions.

## So, what to do? 

1. G﻿o without
2. M﻿anual
3. 3﻿rd Party
4. P﻿owerShell Scripts
5. M﻿IM
6. E﻿ntra ID Cloud Sync
7. E﻿ntra ID Connect Sync

### G﻿O Without

D﻿o you really need the contacts and/or groups from your tenant to go to the other tenant? If not, then yeah! 

Y﻿ou probably don't need the contacts but you might need the groups. If not, then done after implementing Cross Tenant Sync.

D﻿o you need the groups as contacts just for emailing to them or do you need them as Groups with the membership replicated? Do you want the membership flows to be bi-directional?

### M﻿anual

If it is not very many groups and they are to be contacts, then manual might be the best option.

### 3﻿rd Party

I﻿f money is no object then a 3rd party solution can work nicely

### P﻿owerShell Scripts

I﻿f time is no object then writing and maintaining your own PowerShell Scripts can work out.

### M﻿icrosoft Identity Manager 2016 (MIM)

M﻿IM can definitely do the job, but its extended support ends Jan 9, 2029. So, if your GalSync period is short (i.e. after a merger and before consolidation) then this can work.

### E﻿ntra ID Cloud Sync

E﻿ntra ID Cloud Sync can connect to multiple disconnected forests however it does not let you read in groups, and you definitely can't use it to create contacts. I am sure the underlying technology can, but Microsoft has not exposed this through the UI.

### Entra ID Connect Sync

Y﻿ou could use Entra ID Connect Sync. Create a Microsoft PowerShell MA to read from the other tenant and then with some custom sync rules you can get these groups and/or contacts into your tenant. You can choose whether groups will be groups or contacts. One-way syncing of membership is not too difficult. Yes, a PowerShell script is still needed but all of the fussy bits about changes are taken care of by the Sync Engine. We have done this for several clients.

![](/img/galsync-using-entra-id-sync-server.svg)