---
title: 'MIM Join and spaces'
date: 2018-05-05T09:58:00.001-07:00
draft: false
url: /2018/05/mim-join-and-spaces.html
tags: 
- #SQL
- #FIM
- #MIM
---

Working on a customer's lab and look what I found. They had created (through some other process) two user accounts for the same user, and the samAccountName was nearly identical, just a space, ascii 32, appended to the end of one of the samAccountNames differentiates the two. Apparently, AD allows this.  
  
The account with the space was projected into the Metaverse, and then later in the sync the account without the space attempted to join, and it matched. The join failed because of the ambiguous import flow error. But samAccountName "myuser1" matched samAccountName "myuser1 " already in the metaverse.  
  
Turns out this is a feature of SQL. Not just SQL Sever but the ANSI SQL spec created in 1992 [ANSI/ISO SQL-92 specification (Section 8.2, , General rules #3)](https://support.microsoft.com/en-us/help/316626/inf-how-sql-server-compares-strings-with-trailing-spaces).  
  
Wow! So be aware that everywhere in SQL that we do a string comparison and one side has a trailing space or more it will show up as equal. So the consequence of this to MIM users is that when joining it will treat two strings one of which has trailing spaces as equal and try to join them.  
  
Moral of the story: don't rely on trailing spaces to be the differentiator anywhere in any kind of data.  
  

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices