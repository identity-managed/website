---
title: 'Secrets of the Metaverse Part 3'
date: 2013-02-18T05:10:00.001-07:00
draft: false
url: /2013/02/secrets-of-metaverse-part-3.html
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

Many times people wonder how many attributes they can create in the Metaverse Designer tool.

The answer is confusing because ... it depends.

Per my calculations there is a hard limit for single-valued, non-reference attributes of 502. Now to show you my work (in school my math teachers always insisted that I show my work).

Remember from [Part 2](http://blog.ilmbestpractices.com/2013/02/secrets-of-metaverse-part-2.html) that the Metaverse consists of 5 tables:

When you create a new single-valued, non-reference attribute using the Metaverse Designer tool FIM modifies not just data but the table structure of three of these tables: mms\_metaverse, mms\_metaverse\_lineagedate, and mms\_metaverse\_lineageguid. FIM will add a column to each of these tables. The mms\_metaverse table will get a column of a datatype  based on what has been selected as the attribute data type:

Metaverse DataType

SQL Data Type

Min Size

Max Size

Comments

String (Indexable)

nvarchar(448)

2

898

 

String (non-Indexable)

nvarchar(max)

 

2 GB

If the data is small (less than 4000 bytes or whatever limit is set) and doesn't cause the row to exceed the 8060 byte limit it will stored in the row, otherwise only pointers will be stored in the row and the data will be stored in its own set of pages (off-row).

Binary(indexable)

varbinary(900)

2

902

 

Binary(non-indexable)

varbinary(max)

 

2 GB

see the note on string non-indexable

Boolean

bit

1/8

1

If there are between 1-8 bit columns in the table 1 byte of storage is consumed, if 9-16 bits then 2 bytes, if 17-24 then 3 bytes and so on

Number

BigInt

8

8

 

In the mms\_metaverse\_lineagedate table FIM adds a new column of type DateTime which takes 8 bytes. In the mms\_metaverse\_lineageguid table FIM adds a column of type UniqueIdentifier which takes 16 bytes.

A row in SQL Server 2000 and beyond can only hold 8060 bytes. With SQL 2005 and beyond there is a feature called row overflow that allows for the variable length columns (like varchar) to overflow to other pages. However that doesn't apply to fixed length data types like BigInt, DateTime and UniqueIdentifier.

So the mms\_metaverse\_lineageguid has two columns (row\_key a bigInt and object\_id a unique identifier so 24 bytes) and then one column of type UniqueIdentifier for every single-valued non-reference attribute. 8060-24 = 8036 and 8036/16 = 502.25, which rounds down to 502.

So while there may be other limits that may depend on the datatype selected, this is one limit that cannot be escaped.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices