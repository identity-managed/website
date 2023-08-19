---
title: 'FIM 2010 -- Update Rollup 2 4.0.3606.2'
date: 2012-02-28T09:32:00.001-07:00
draft: false
url: /2012/02/fim-2010-update-rollup-2-4036062.html
tags: 
- Forefront Identity Manager
- Identity Management
- FIM
---

[FIM 2010 Update Rollup 2](http://support.microsoft.com/kb/2635086) is now available. [Download from here](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=forefront%20identity%20manager)

Before blindly applying this update it is critical that you read the release notes, as XMA's or ECMA's may not run after the update. If you changed the MIISServer.exe.config file to tweak the FIM MA performance the update won't replace your file. So you have to make some updates to it by hand. This is documented in the [release notes](http://support.microsoft.com/kb/2635086).

There are lots of fixes, my most favorite is that they have rolled back the change I mentioned \[ranted about\] in a previous blog post: [What the %\_ is the deal with wildcards in FIM Queries in the latest hotfix?](http://blog.ilmbestpractices.com/2011/11/ok-i-am-not-actually-swearing-nor-are.html)

My next favorite new feature and this one alone will get a separate blog entry, is the release of the ECMA 2.0 ([information available on the beta and RC of the ECMA 2.0 here](https://connect.microsoft.com/site433/Downloads/DownloadDetails.aspx?DownloadID=37582)).

A few sync engine crash issues have been fixed.

Support for writing rules extensions in .NET 4.

**Update to the update: Do not run the stored procedure mentioned below, it can result in incorrect set query results.**

**Update:** The KB article was updated today and the item dealing with this stored procedure mentioned below has been **removed**. You should know that this stored procedure is intended to solve a specific performance problem and should only be implemented with guidance from PSS. You should also know that running it is a **one-way trip** i.e. the only way to undo it is to restore the FIMService database from backup.

Another key item that once more underscores the need to read the release notes, is a fix for the FIM Service dealing with large criteria based sets and groups. In order to take advantage of this performance enhancement it is necessary to run a stored procedure (EXECUTE \[fim\].\[EnableSetPartitioningAndTabularFunctions\]) by hand. Based on the name I expect that this procedure is doing some table partitioning, more on that when I get a chance to take a look. (Please see the update above)

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices