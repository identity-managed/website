---
title: 'Secrets of the Metaverse Part 5'
date: 2013-03-22T15:42:00.001-07:00
draft: false
url: /2013/03/secrets-of-metaverse-part-5.html
tags: 
- Forefront Identity Manager
- FIM 2010 R2
- FIM
---

Parts 1-5:

1.  [What is the Metaverse?](http://blog.ilmbestpractices.com/2013/02/secrets-of-metaverse-part-1.html)
2.  [How is the Metaverse data stored?](http://blog.ilmbestpractices.com/2013/02/secrets-of-metaverse-part-2.html)
3.  [Is there a limit to how many Metaverse attributes I can have?](http://blog.ilmbestpractices.com/2013/02/secrets-of-metaverse-part-3.html)
4.  [Has access to the metaverse gotten faster with recent releases?](http://blog.ilmbestpractices.com/2013/03/secrets-of-metaverse-part-4.html)
5.  [How do I safely query the metaverse?](http://blog.ilmbestpractices.com/2013/03/secrets-of-metaverse-part-5.html)
6.  Added (Aug 5 2015): [How Many Metaverse Attributes can I have?](http://blog.ilmbestpractices.com/2015/08/how-many-attributes-can-you-have-in.html)

First of all the FIM Product group does not support direct modification of the data in any of the FIM databases. Do so can leave your database in a state that is entirely unsupportable.

Second, the FIM Product group doesn't support direct queries against any of the FIM databases. However, it is possible to query the FIM Synchronization Service database without causing problems and without enormous gyrations. The FIM Service database has a very \*interesting\* data structure and is much more difficult to query.

**So how do you safely query the FIM Synchronization Service database?**

1) Use **no lock** hint

or

2) Set the transaction isolation level to **read uncommitted**.

Both of these tell SQL to not obtain locks on the records you are querying. This means that other threads such as the one that is synchronizing records don't get stuck waiting on your query. However this does also mean that some of the data you read could be in the middle of transaction, a transaction that could be rolled back. For example you query could catch it at the moment when a new MV object has just been projected from the HR MA but has not yet provisioned to AD. That transaction could succeed and commit or it could get rolled back and the MV project undone.

On to the how:

To use the no lock hint you must place it after every table and view name referenced in your query like this:

SELECT MetaverseObjectCount, ConnectorSpaceObjectCount, MetaDirectoryObjectCount = MetaverseObjectCount  + ConnectorSpaceObjectCount  
FROM (select count(\*) AS MetaverseObjectCount  
    FROM MicrosoftIdentityIntegrationServer.dbo.\[mms\_metaverse\] **with (nolock)**) as MVC  
CROSS JOIN  
(select  count(\*) AS ConnectorSpaceObjectCount

FROM MicrosoftIdentityIntegrationServer.dbo.\[mms\_connectorspace\] **WITH (nolock)** ) AS CSOC

To Set the transaction isolation level to **read uncommitted** you simply run that command and the keyword GO before your queries -- sometimes your reporting tools permit you to set that with a checkbox

**set transaction isolation level read uncommitted  
**go

SELECT MetaverseObjectCount, ConnectorSpaceObjectCount, MetaDirectoryObjectCount = MetaverseObjectCount  + ConnectorSpaceObjectCount  
FROM (select count(\*) AS MetaverseObjectCount  
    FROM MicrosoftIdentityIntegrationServer.dbo.\[mms\_metaverse\] ) as MVC  
CROSS JOIN  
(select  count(\*) AS ConnectorSpaceObjectCount

FROM MicrosoftIdentityIntegrationServer.dbo.\[mms\_connectorspace\]  ) AS CSOC

One might ask: Can you do both? Yes you can and it will cause no harm. The one place you can use the set transaction isolation level command is in a view or stored procedure -- so inside of those objects you must use the WITH (nolock) hint

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices