---
title: What does MIM's StoreChk.exe do?
description: Explains MIM's StoreChk.exe does
tags:
  - MIM
  - storechk
date: 2024-03-29T00:13:51.610Z
banner: /img/mimsyncstorecheck_custom.png
---
I﻿ watched through SQL Profiler to better understand what these checks do, and I found an error with check #10. It says it is "Checking Lineage Guid table for MV objects with invalid MV object ids" but the SQL query it issues is the same as the query for Check # 9 "Checking Lineage Date table for MV objects with invalid MV object ids." It queries the Lineate Date table instead of the Lineage GUID table like it says.

```sql
SELECT object_id FROM mms_metaverse 
	 WHERE (NOT EXISTS (SELECT object_id FROM mms_metaverse_lineagedate 
                        WHERE  mms_metaverse.object_id=mms_metaverse_lineagedate.object_id))

SELECT object_id FROM mms_metaverse 
	 WHERE (NOT EXISTS (SELECT object_id FROM mms_metaverse_lineagedate 
                        WHERE  mms_metaverse.object_id=mms_metaverse_lineagedate.object_id))
```

I﻿ also noticed that after #19 "Checking Step History table for invalid run history ids" it does not check Step Object Details table for invalid step history ids. I have an instance with over 7.6 M records of Step Object Details that don't have a valid step history id. Clearing run history does not seem like it will get to these since those queries look for Step Object Details records related to Step History records related to Run History records within a certain time frame. So here is my suggested query (I am placing this query is in the public domain): 

```sql
SELECT count(*) as SODs_whose_SHIDs_dont_Exist
  FROM [mms_step_object_details] sod with (nolock)
  where NOT EXISTS (SELECT 1 FROM mms_step_history sh with (nolock)
	where sh.step_history_id = sod.step_history_id)	 
```

MMS Store Analysis Tool (v4.6.673.0) does 24 different checks:

1. Checking for CS objects with invalid MA IDs:  
2. Checking for CS objects with invalid parent ids:
3. Checking CS Link table for CS objects with invalid source CS object IDs:
4. Checking CS Link table for CS objects with invalid ref CS object IDs:
5. Checking CSMV Link table for Links with invalid CS object IDs:
6. Checking CSMV Link table for Links with invalid MV object IDs:
7. Checking MV Link table for MV objects with invalid source MV object IDs:
8. Checking MV Link table for MV objects with invalid ref MV object IDs:
9. Checking Lineage Date table for MV objects with invalid MV object ids:
10. Checking Lineage Guid table for MV objects with invalid MV object ids:
11. Checking Lineage Date table for objects with invalid MV object ids:
12. Checking Lineage Guid table for objects with invalid MV object ids:
13. Checking MV Multivalue table for objects with invalid MV object ids:
14. Checking MV Multivalue table for duplicate numeric_value values:
15. Checking MV Multivalue table for duplicate string_value_indexable values:
16. Checking MV Multivalue table for duplicate binary_value_indexable values:
17. Checking Run Configuration table for invalid MA ids:
18. Checking Run History table for invalid MA ids:
19. Checking Step History table for invalid run history ids:
20. Checking Lineage Cross Reference table for invalid MA ids:
21. Checking CS for connectors which have no CSMV link.:
22. Checking Partition table for invalid MA ids:
23. Checking synchronization rule and MA rules consistency:
24. Checking links on all CS objects: