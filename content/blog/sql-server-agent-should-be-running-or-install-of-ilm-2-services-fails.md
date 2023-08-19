---
title: 'SQL Server Agent should be running or install of ILM 2 Services fails'
date: 2008-10-22T20:52:00.001-07:00
draft: false
url: /2008/10/sql-server-agent-should-be-running-or.html
tags: 
- ILM
- ILM 2 Beta 3
- SQL Server
---

I posted the following to the Community Content Section of the [ILM 2 Beta 3 Installation Guide](http://technet.microsoft.com/en-us/library/cc561135.aspx)

The SQL Agent Service account must be a sql sysadmin and the SQL Agent Service must be running or during install you may get "error -2147217900

Failed to execute sql string addtemporaleventsjobtoSQLServer" while trying to install ILM 2 Beta 3 Identity Management Platform Services. Apparently, the install routine needs to create a SQL Agent Job and with SQL 2005 the Agent must be running to create a job.

The job it creates is called ILM\_TemporalEventsJob and according to its description it "Periodically identify workflows to be run on objects that have transitioned to or from temporal sets." It is scheduled to be run every day at 1 AM.

It has only one step of type T-SQL: EXEC dbo.TriggerTemporalEvents. So later on if you find that objects are not getting transitioned to and from temporal sets you might need to come and check this job's history, and ensure that the SQL Agent is running.

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/SQLServerAgentshouldberunningorinstallof_1247A/image_thumb.png)](http://www.ilmbestpractices.com/blog/uploaded_images/SQLServerAgentshouldberunningorinstallof_1247A/image.png)

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices