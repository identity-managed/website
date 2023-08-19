---
title: 'When moving the FIM DB ensure FT Indexing enabled'
date: 2010-09-04T06:39:00.001-07:00
draft: false
url: /2010/09/when-moving-fim-db-ensure-ft-indexing.html
tags: 
- Forefront Identity Manager
- FIM
---

I just found a very intriguing blog post from [Thomas](http://setspn.blogspot.com/) Vuylsteke, about a potential danger when moving your FIM Service Database from SQL Server to another: [The case of the new attributes that didn’t want to be found](http://setspn.blogspot.com/2010/09/case-of-new-attributes-that-didnt-want.html "The case of the new attributes that didn’t want to be found")

In short there is the potential that when you move the database that it might arrive on the new server with the Full Text Indexing disabled. The way Thomas tumbled to the problem was that he couldn’t search for a new attribute.

His post has a clever title and is well written, exposing a potential problem.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices