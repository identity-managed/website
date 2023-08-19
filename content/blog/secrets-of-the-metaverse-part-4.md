---
title: 'Secrets of the Metaverse Part 4'
date: 2013-03-11T14:44:00.001-07:00
draft: false
url: /2013/03/secrets-of-metaverse-part-4.html
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

Has access to the metaverse gotten faster with recent releases? Well I won't cover everything they have done but two really significant things:

1) Skinnier clustered index key for the mms\_metaverse table:

2) Sequential numbering of the clustered index key

1) Skinnier clustered index key for the mms\_metaverse table:

 

Old

New

column used as the clustered Index key:

object\_id

row\_key

DataType:

uniqueIdentifier

big\_int

Size:

16 bytes

8 bytes

The mms\_metaverse table previously used the object\_id column of type uniqueIdentifier (16 bytes) as the clustered index key. The product group added a new column called row\_key of type big\_int (8 bytes).

So how does this help?

Think of a database table like a book. The clustered index is the Table of Contents and the main text of the book, excluding the indexes in the back. There is only one order for the book to go in and that is the same with a table. In the book the key used in the table of contents is the page #. In a table we pick one or more columns to serve as the clustered index key.

The non-clustered indexes are like the indexes in the back of the book (a topical index, a place index, a person index) and they make include the clustered index key. So the topical index lists a subject and then the page(s) where it is found.

Clustered Index ~ Table of Contents

Clustered Index Key ~ page number

Non-Clustered Index ~ Topical Index at the back of the book

Non-Clustered Index Key ~ topic

Pretend we had to pad the page # so it looked like 00000000045?

Chapter 1 page 0000 0000 0000 0000 0000 0000 0001

Chapter 2 page 0000 0000 0000 0000 0000 0000 0093

Then the topical index would look like (the topical index includes the key from the table of contents -- the page number):

Beach 0000 0000 0000 0000 0000 0000 0006

Desert 0000 0000 0000 0000 0000 0000 0020

Suddenly this limits how many columns of the index I can print on a single page.

Both the table of contents and the index are much larger consuming more pages. It also takes more time to search through those pages for my topic.

By going to a skinnier clustered index key it is as though the product group changed the book to be like this:

Chapter 1 page 0001

Chapter 2 page 0093

and the index to this:

Beach 0006

Desert 0020

Suddenly the table of contents and the index take fewer pages and it is faster to leaf through them when searching. So it is with a database table reading the table and its indexes is now much faster.

2) Sequential numbering of the clustered index key

This new column has data populated automatically using the SQL Server identity feature (this feature allows new rows to be added with an incrementing counter). Previously new pages would be inserted in random order and sometimes that mean splitting pages.

So how does this help?

The use of an identity column to increment 1 by 1 as opposed to a randomly generated unique identifier is enormously helpful in writes and will lead to less fragmentation. Whereas prior to the change a new row could be inserted anywhere in the entire table, now it will be inserted at "the end."

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices