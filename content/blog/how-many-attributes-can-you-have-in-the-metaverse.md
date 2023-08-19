---
title: 'How many attributes can you have in the Metaverse?'
date: 2015-08-05T19:58:00.005-07:00
draft: false
url: /2015/08/how-many-attributes-can-you-have-in.html
tags: 
- SQL
- Forefront Identity Manager
- MIIs
- ILM
- Microsoft Identity Manager
- MIM
- FIM
---

Back in 2013 I published 5 posts about the [Secrets of the Metaverse](http://blog.ilmbestpractices.com/2013/02/secrets-of-metaverse-part-1.html):

Parts 1-5:

1.  [What is the Metaverse?](http://blog.ilmbestpractices.com/2013/02/secrets-of-metaverse-part-1.html)
2.  [How is the Metaverse data stored?](http://blog.ilmbestpractices.com/2013/02/secrets-of-metaverse-part-2.html)
3.  [Is there a limit to how many Metaverse attributes I can have?](http://blog.ilmbestpractices.com/2013/02/secrets-of-metaverse-part-3.html)
4.  [Has access to the metaverse gotten faster with recent releases?](http://blog.ilmbestpractices.com/2013/03/secrets-of-metaverse-part-4.html)
5.  [How do I safely query the metaverse?](http://blog.ilmbestpractices.com/2013/03/secrets-of-metaverse-part-5.html)
6.  Added (Aug 5 2015): [How Many Metaverse Attributes can I have?](http://blog.ilmbestpractices.com/2015/08/how-many-attributes-can-you-have-in.html)

  
The [third post was about how many attributes you can have in the Metaverse](http://blog.ilmbestpractices.com/2013/02/secrets-of-metaverse-part-3.html) in which I said that the mms\_metaverse\_lineageguid table **limits us to 502 single valued non-reference attributes in the Metaverse**. This is still correct but a client told me of a scenario they encountered where the lineageguid table prevented them from getting to over **450 attributes** and they encouraged me to blog about how they solved it.  
  
The issue can occur when you delete attributes from the Metaverse and then try to add more. **If you exceed 502 single valued non-reference attributes that have ever existed in your Metaverse** you will encounter this error unless you take some very specific actions at the database level. WARNING: these actions should be done under the direction of Microsoft Support so that your installation can remain in a supported state.  
  
The client had deleted a number of unused attributes prior to adding the many attributes they needed and then hit a brick wall getting the following error in their application event log:  

>  0x8023042e (the table cannot be created because the row size limit was exceeded.):SQL: ALTER TABLE \[dbo\].\[mms\_metaverse\_lineageguid\] ADD \[theirAttribute\] \[uniqueidentifier\] NULL 0x80230629 (the specified metaverse schema has too many attributes).

  
First: Why does this happen?  
As you can see from the error message when you add or delete a single valued non-reference attribute to the Metaverse the Synchronization Service runs an ALTER TABLE statement to add or delete a column and as famed [SQL MVP and author Kalen Delaney states](http://sqlblog.com/blogs/kalen_delaney/archive/2006/10/13/alter-table-will-not-reclaim-space.aspx) running "ALTER TABLE will not reclaim space." Her article is about altering the length of column but ["Database Whisperer" Michael J Swart provides an example of removing columns](http://michaeljswart.com/2010/02/removing-columns/) and shows that ALTER TABLE just makes a meta data level change. So even though the column is not used anymore it is still taking up space in the table until the Clustered Index is rebuilt.  
  
You can see how close you are getting by using the following query (I used Michael's and Kalen's queries as starting points):  
  

> USE FIMSynchronization  
> GO  
> SELECT  c.name AS \[Column Name\], column\_id, leaf\_offset, pc.is\_dropped  
>  FROM sys.system\_internals\_partition\_columns pc  
>     JOIN sys.partitions p  
>         ON p.partition\_id = pc.partition\_id  
>    LEFT JOIN sys.columns c  
>          ON column\_id = partition\_column\_id  
>             AND c.object\_id = p.object\_id  
> WHERE p.object\_id=object\_id('mms\_metaverse\_lineageguid')  
> ORDER BY pc.leaf\_offset  
> GO

  

Column Name Column\_ID Leaf\_Offset Is\_Dropped

\------------------ -------------   ---------        --------------

title                  99              1564           0  
type                  100              1580           0  
uid                  101              1596           0  
NULL          NULL      1612           1  
NULL          NULL      1628           1  
testAttribute3  105              1644           0  
  
In this example I have added three attributes and then deleted two of them (the first two I added). As you can see this leaves behind some open space in the mms\_metaverse\_LineageGuidtable and means that I would hit the limit sooner than I would expect.  
  
If the biggest Leaf\_Offset is **8044** then **you are out of space** to add more single value non-reference attributes (8044 byte offset+16 bytes =8060 bytes limit for a SQL row).  
  
Normally, rebuilding the clustered index will reclaim the space for you. So you think no problem since you have followed my advice in FIM Best Practices Volume 1 and you use Ola Hallengren's scripts to automate index maintenance. However, the script will only rebuild if the index is more than 30% fragmented otherwise it will just reorganize it (which doesn't reclaim the space). So you could rebuild the clustered index by hand. Oops! The mms\_metaverse\_LineageGuid table doesn't have a clustered index -- so you have to add one. But then to return the database schema to its supported state you need to drop the clustered index. You can the clustered index on the object\_ID column as this will be unique and not null. Then drop it.  
  
 ONCE AGAIN: ONLY DO THIS UNDER THE DIRECTION OF MICROSOFT SUPPORT if you want to stay supported (and with all Syncs halted).  
  

> CREATE CLUSTERED INDEX \[CX\_mms\_metaverse\_lineageguid\_object\_id\] ON dbo.mms\_metaverse\_lineageguid ( object\_id)

  

> GO

  

> DROP INDEX \[CX\_mms\_metaverse\_lineageguid\_object\_id\] ON dbo.mms\_metaverse\_lineageguid

  
The creating or dropping of a clustered index forces the rebuilding of any non-clustered indexes. Unfortunately that means that this happens twice. But that can not be avoided. For a big table that can take a while (tens of minutes for metaverse with hundreds of thousands of rows). Of course the pure DBA would prefer to create an appropriate Cluster Index and leave it, rather than drop it, but that would put me out of support by the MIM product group.  
  
When I rerun the query I get:  
  

Column Name Column\_ID Leaf\_Offset Is\_Dropped

\------------------ -------------   ---------        --------------

title                  99              1564           0  
type                  100              1580           0  
uid                  101              1596           0  
testAttribute3  105              1612           0  

  

You can see that testAttribute3 is now offset at 1612 and the other columns are gone. Now that space is available to use for the lineageguids of attributes. 

  

So that is how you reclaim the space so you can add more attributes.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices