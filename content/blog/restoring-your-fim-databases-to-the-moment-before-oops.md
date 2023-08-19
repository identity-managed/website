---
title: 'Restoring your FIM databases to the moment before oops'
date: 2010-05-20T10:04:00.001-07:00
draft: false
url: /2010/05/restoring-your-fim-databases-to-moment.html
tags: 
- Backups
- Forefront Identity Manager
- SQL Server
- FIM
---

At the FIM Birds of a Feather (BOF) after a discussion about FIM database backups I was asked to make a blog post to more fully elucidate the benefits of using the full recovery model.

Since Recovery models affect the transaction log you may find it useful to have the following background about transaction logs:

•The Data in tables and indexes are stored in data files not the transaction log

•The Transaction Log (T-Log) is like a court stenographer, serially noting down everything that took place without sorting/cataloging

• This gives SQL Server Reliability, recoverability and speed because as data changes happen they happen on the Data pages loaded into RAM and to the T-Log on disk (done in a quick serial fashion)

•Upon checkpoint (approx 1/min) changed pages are written to data files

The first thing to note is that there are three recovery models for SQL Databases, but you will find yourself choosing between Full and Simple, as Bulk-Logged is one that is used temporarily.

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/RestoringyourFIMdatabasestothemomentbefo_8D82/image_thumb.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/RestoringyourFIMdatabasestothemomentbefo_8D82/image.png)

There are also 3 backup types:

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/RestoringyourFIMdatabasestothemomentbefo_8D82/image_thumb_3.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/RestoringyourFIMdatabasestothemomentbefo_8D82/image_3.png)

If you are in Simple you can not backup the Log

If you are in Full you must backup the log, because after your first full backup the log will begin to fill up and will not empty itself (truncate) until you perform a log backup or switch the database to Simple.

The benefit to being in full is that you can then restore your databases to a moment in time.

So let’s say that you are doing a long running initial load process into the FIM Service database, or you just get done and then you begin something new and to your horror you realize that you just imported from a test system into production FIM. Or you were moving over config from test to prod and it goofed up. Well back in the ILM days you could clear your connector spaces and reload. You can do that today although I was told that you shouldn’t ever clear the FIM MA connector space. Additionally reloading data into the FIM Service can be quite time consuming.

So it can much more productive to restore the affected database right up to the moment before the disaster. You may need to restore both databases to the same moment or only one maybe affected. I will illustrate with one.

The first step is to confirm the time at which you want to stop by examining the request history in the FIM Service or in the Synchronization Service Manager.

Next stop the appropriate Services.

From here on this is a sql script and all directions are prefaced with double dashes to make the comments in T-SQL

\--Perform a log backup with no truncate, some refer to this as an emergency log backup or backup the tail of the log

Backup Log FIMService To Disk = 'c:\\sqlbackups\\FIMService\_taillog.bak' With NO\_TRUNCATE, NORECOVERY

\--Next is to restore your latest full backup (you will need to ensure that no one is connected to the database)

Restore Database FIMService From Disk = 'c:\\sqlbackups\\FIMService\_full.bak' with NORECOVERY, stats=10

\--The no\_recovery option tells sql that you have more to restore and not make the database available yet

\-- Then restore all of the intervening transaction log backups in order since the full backup and leading up to but not including the log backup with no truncate.

Restore Log FIMService From Disk = 'c:\\sqlbackups\\FIMService\_log1.bak' with NORECOVERY, stats = 10

\-- You will need to repeat the above command for every transaction log backup since the full but not including the tail

\--Finally restore the tail and here is the magic

Restore Log FIMService From Disk = 'c:\\sqlbackups\\FIMService\_taillog.bak' with NORECOVERY, stats = 10, STOPAT = 'Mar 15, 2010 12:15:23 AM’

RESTORE DATABASE FIMService WITH RECOVERY

\-- Then restart the appropriate services

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices