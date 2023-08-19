---
title: 'How to import the Domain attribute into the FIM Portal Part 2'
date: 2012-08-16T13:46:00.001-07:00
draft: false
url: /2012/08/how-to-import-domain-attribute-into-fim_16.html
tags: 
- Forefront Identity Manager
- FIM 2010 R2
- FIM
---

In [Part 1 of How to import the Domain attribute into the FIM Portal](http://blog.ilmbestpractices.com/2012/08/how-to-import-domain-attribute-into-fim.html) I provided you the simple technique for the single domain forest, and the technique that works although is a bit unwieldy – that of looking at the first 41 characters of the object’s SID and using a lookup table through nested IIF statements and this doesn’t .

What if there was a simpler way?

What about using the Domain Component option in the attribute flow?

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/fb0eb65f2cf7_B425/image_thumb.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/fb0eb65f2cf7_B425/image.png)

Well the problem is that the component starts from left and goes to the right, so if you have objects of varying OU depth, you can’t use this to get what you need reliably. You can use this to get the rDN but that is all. If only you could input negative numbers to tell it to go right to left that would be something. But then that would still have problems with domains of varying depths.

Of course this wouldn’t work if the NetBios Domain Name is not the first domain component of the DN. For example, SnappySlackers.com but NetBios Name of HQ.

What about all of those functions in the Sync Rules? Can we use those? Yes.

If we replace the “,DC=” with the | and use the Word function to split it up and grab the one we want.

Word(ReplaceString(dn,",DC=","|"),2,"|")

What if the DC= comes across as lower case? What if one of the OU’s contains the pipe character:

**Word(ReplaceString(ReplaceString(UpperCase(dn),"|"," "),",DC=","|"),2,"|")**

Although we still face the same exception about NetBios Domain Name, we can use IIF to handle the exceptions. So if SnappySlackers.com has a netbios domain name of HQ but all of the others have a corresponding NetBios Domain name such as NA.SnappySlackers.com is NA and EMEA.SnappySlackers.com is EMEA then the following would work and would even handle new domains as long as the NetBios Domain Name and the first Domain Component match.

IIF(Eq(Word(ReplaceString(ReplaceString(UpperCase(dn),"|"," "),",DC=","|"),2,"|"),”snappyslackers”),”HQ”,Word(ReplaceString(ReplaceString(UpperCase(dn),"|"," "),",DC=","|"),2,"|")

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices