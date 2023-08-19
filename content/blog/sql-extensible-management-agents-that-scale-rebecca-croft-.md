---
title: 'SQL Extensible Management Agents That Scale (Rebecca Croft)'
date: 2011-06-23T15:27:00.001-07:00
draft: false
url: /2011/06/sql-extensible-management-agents-that.html
tags: 
- Forefront Identity Manager
- Identity Management
- TEC
- FIM
- #TEC2011
---

[Rebecca](http://www.apollojack.com/), a fellow Ensynchian, presented at TEC 2011 on the limitations of the standard out of the box SQL Management and how she overcame them by writing a very fast eXtensible Management Agent (XMA).

First attempt use ado.net sql reader to read data (really fast) and write one row at a time to the AVP file (but that gets slow when dealing with large data sets).

Second attempt use the T-SQL “FOR XML” clause to transform the data to XML and then use an XSLT to transform to LDIF.

So the XMA executes a T-SQL statement to export the data to XML and then XSLT to transform to LDIF and then returns the LDIF file to the FIM Synchronization Service.

She even showed off a wizard to create the XMA for us. When it completed successfully she received a spontaneous round of applause.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices