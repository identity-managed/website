---
title: 'Files, FIM, and PowerShell (James Booth)'
date: 2011-04-18T11:38:00.001-07:00
draft: false
url: /2011/04/files-fim-and-powershell-james-booth.html
tags: 
- Forefront Identity Manager
- Identity Management
- TEC
- FIM
- #TEC2011
---

James Booth former Microsoft Group Program Manager for MIIS (precursor to FIM) presented on using PowerShell to process files in preparation for consumption by FIM.

James points out that “In the beginning, it was all files.” These call based MA’s are the new kids on the block, also said that at Microsoft in 2000 the philosophy was “XML is the answer, now what is your question?”

James has posted his new commandlets to GitHub [https://github.com/jhbooth/LDIF-PowerShell](https://github.com/jhbooth/LDIF-PowerShell) 

Commandlet

Description

Import-DirectoryCredential

Imports directory credentials from a file, and returns a custom PowerShell object. Imports directory credentials from a file created using Export-DirectoryCredential

Export-DirectoryCredential

see above

Import-LDIF

Imports directory information from an LDIF file, and writes custom PowerShell objects to the pipeline.

Export-LDIF

Exports directory information from the pipeline to an LDIF file

Convert-EscapeDnComponent

Escape DN components – escaping

James also talked about “munging” the data by piping the data through other functions to transform the data.

He also cautioned against thinking that PowerShell is the only way to do something.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices