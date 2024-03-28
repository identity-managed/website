---
title: MIM StoreChk.exe Assumes SQL is Local
description: How to use MIM Sync StoreChk when SQL Server is remote
tags:
  - MIM
  - StoreChk
date: 2024-03-28T18:55:15.198Z
banner: /img/mimsyncstorecheck_custom.png
---
On occasion you may need to verify the integrity of the MIM Synchronization Service Database. To do this you can use the Store Check tool, StoreChk.exe located in the bin folder under the root of your MIM Synchronization install.

W﻿hile the storechk tool does read the registry to find the name of the database (almost always is FIMSynchronizationService) it does not read the Server or Instance name registry values in the parameters key of the registry. Instead it defaults to assume that the SQL Server is co-located on the same machine as MIM Sync. 

S﻿ince this installation is not colocated we kept getting this error:

MMS Store Analysis Tool (v4.6.673.0) starting...

FAILED: hr = 0x80230406 OLEDB Provider Information:
Description  = 'Login timeout expired'
Failure Code = 0x80004005
Minor Number = 0

W﻿e even used Process Monitor from SysInternals to see that it read the registry for the DB Name but did not see it read the ServerName value (which has the name of the SQL Server).

S﻿o we experimented a few times and found that -Server will make it work to talk to a remote SQL Server:

storechk.exe -Server CompanySQLServer