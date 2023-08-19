---
title: 'Searching an entire database for a Guid or Unique Identifier'
date: 2010-06-01T08:47:00.001-07:00
draft: false
url: /2010/06/searching-entire-database-for-guid-or.html
tags: 
- SQL
- T-SQL
---

Searching an entire database for a Guid or Unique Identifier can be a bit of a tricky proposition. However a little bit of using T-SQL to generate T-SQL and viola

DECLARE @GUIDHunted nvarchar(60)  
SET @GUIDHunted = '0A24EC0C-65EE-4519-89DF-ABD3DD24F7EF'

SELECT \*, 'UNION ALL SELECT ''' + s.name + '.'  +  ao.name + ''', count(\*) FROM '  
\+ s.name +'.\[' + ao.name  + '\] WHERE ' + ac.name + ' = ''' + @GuidHunted + ''''  
FROM sys.all\_columns ac  
JOIN sys.all\_objects ao  
    ON ac.\[object\_id\] = ao.\[object\_id\]  
JOIN sys.schemas s  
    ON ao.\[schema\_id\] = s.\[schema\_id\]   
where user\_type\_id = 36 -- UniqueIdentifier  
and s.name != 'sys'

Here is the output result for a fictional database (just copy the results into a new query window, delete the first UNION ALL and execute).

UNION ALL SELECT 'myschema.Objects' , count(\*) FROM myschema.Objects WHERE ObjectID = '0A24EC0C-65EE-4519-89DF-ABD3DD24F7EF'

UNION ALL SELECT 'myschema.Objects2' , count(\*) FROM myschema.Objects2 WHERE ObjectID = '0A24EC0C-65EE-4519-89DF-ABD3DD24F7EF'

This assumes that programmers weren’t storing guids in nvarchar types or that the programmers didn’t create other user types using unique identifiers

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices