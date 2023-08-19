---
title: 'FIM Reporting Craig Martin style'
date: 2012-05-01T12:10:00.001-07:00
draft: false
url: /2012/05/fim-reporting-craig-martin-style.html
tags: 
- SQL
- Forefront Identity Manager
- FIM 2010 R2
- #TEC2012
- FIM
---

Craig’s session is on how to get data out from the FIM Service and FIM Sync with PowerShell and displaying it with SSRS, which he has dubbed Scissors!

Ok Craig we get it! You have even persuaded me that PowerShell is important! I have started writing scripts. SQL Server of course is still important.

Key is to hook up a pipeline from PowerShell to pass into [his custom SSRS PowerShell Data Processing Extension (DPE).](http://psdpe.codeplex.com/) Craig uses export-clixml and import-clixml to serialize data before it is expired from the FIM system.

One thing he does point it is that you can’t use the Report Builder, you must use BIDS to create your reports, because [DPE’s are not supported with Report Builder](http://msdn.microsoft.com/en-us/library/dd239371(v=SQL.100).aspx)

Overall Craig does an excellent job of reusing the tools and capabilities for other areas to show us some really useful stuff with FIM.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices