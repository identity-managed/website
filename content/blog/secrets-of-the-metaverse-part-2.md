---
title: 'Secrets of the Metaverse Part 2'
date: 2013-02-15T06:16:00.001-07:00
draft: false
url: /2013/02/secrets-of-metaverse-part-2.html
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

Where and how is the Metaverse data stored?

Before I get into that I must caution you that modifying data directly will put you in a position that is unsupported by Microsoft. Even querying the data is something of a touchy issue (see [Part 5](http://blog.ilmbestpractices.com/2013/03/secrets-of-metaverse-part-5.html)).

The Metaverse consists of 5 tables in the FIM Synchronization Service Database:

Table

Comment

mms\_metaverse

Every object in the metaverse has a row in this table. Single-Valued non-reference attributes are stored in this table

mms\_metaverse\_lineagedate

This table has a DateTime column of the same name of every attribute column in the mms\_metaverse table (in other words -- single-valued non-reference attributes).

mms\_metaverse\_lineageguid

This table has a UniqueIdentifier column of the same name of every attribute column in the mms\_metaverse table (in other words -- single-valued non-reference attributes).

mms\_mv\_link

Reference attributes (both single valued and multi-valued) are stored in this table in an Entity Attribute Value format. The references are kept as uniqueIdentifiers

mms\_metaverse\_multivalue

Non-Reference multi-valued attributes are stored in this table in an Entity Attribute Value format (with a column for each of the possible data types)

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices