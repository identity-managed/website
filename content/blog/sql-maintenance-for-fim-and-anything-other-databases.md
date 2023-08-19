---
title: 'SQL Maintenance for FIM and anything other databases'
date: 2014-10-24T17:36:00.002-07:00
draft: false
url: /2014/10/sql-maintenance-for-fim-and-anything.html
tags: 
- SQL
- FIM 2010 R2
- FIM
---

  

An easy way to take care for your FIM databases is to "use Ola Hallengren's script ([http://ola.hallengren.com/scripts/MaintenanceSolution.sql](http://ola.hallengren.com/scripts/MaintenanceSolution.sql)). Download the script, adjust the backup paths and run the script on each instance of SQL Server. It will automatically create several jobs some for maintaining the system databases and some for maintain the user databases. You will need to create schedules for each of the jobs." -- FIM Best Practices Volume 1

I love using Ola script for index maintenance because it is so much smart than the Database Maintenance wizard which wants to spend lots of time rebuilding indexes that only needed to be reorganized and messing with indexes that were just fine or too small to matter. A table with less than 1000 pages is usually too small to matter. Less than 5% fragmentation and why bother. Less than 20% and a reorg will usually solve it. Over 20% and you should usually rebuild.

A benefit of using a smart index maintenance solution is that your transaction log backups won't be as large as they would if you rebuild all indexes.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices