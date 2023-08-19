---
title: 'Creating Management Agents with the new EZMA (Andreas Kjellman)'
date: 2011-04-18T13:00:00.001-07:00
draft: false
url: /2011/04/creating-management-agents-with-new.html
tags: 
- Forefront Identity Manager
- Identity Management
- TEC
- FIM
---

At TEC 2011, Andreas Kjellman of Microsoft, who “owns” the FIM synchronization engine, showed off the upcoming EZMA framework.

**The problem:**

The existing eXtensible Management Agent (XMA) does not have a call based import method, we are limited to using GUIDs as the initial anchors, and we don’t have partitions in an XMA.

**Solution**

EZMA – which, IMO, will actually be a little harder to do than an XMA but will allow the developer to do much more that will make the FIM admin’s life easier.

Some of the new features:

**Call based import**, that you can batch! So just like with an AD MA run profile step (see the figure) we can configure batch size and it will actually have an impact, and you can also choose a partition to process.

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/2cd795b5dce4_969D/image_thumb.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/2cd795b5dce4_969D/image.png)

The **call based export** is modified to be able to **batch** it  too. So instead of calling ExportEntry for each csentry object you will get the ExportEntries method which will have a collection of csentry objects that have pending exports.

The schema, partitions and hierarchy can be discovered programmatically.

**Custom anchors** – that aren’t GUIDs.

Even better support for **custom parameters (of different data types)**

Finally the ability to do a **full export**! Which is great when you have a target that doesn’t store state.  However, you must decide at design time which type of exports your MA will be executing.  You can choose either delta or full, but not both.

**Comments**

The XMA will still be supported.

The EZMA is more of a developer activity than the XMA was. Your dev will need to learn new interfaces, but should need to know a little less about the internal workings of the sync engine.

**Bottom Line**

Good move because now we can write EZMA’s that are as fully functional as anything the product group does.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices