---
title: 'What AD Attributes are indexed? ANR? Tuple? PowerShell'
date: 2014-12-04T11:50:00.003-07:00
draft: false
url: /2014/12/what-ad-attributes-are-indexed-anr.html
tags: 
- PowerShell
- AD
---

Import-Module ActiveDirectory  
Write-Host "Tuple Index Enabled Attributes"  
Get-ADObject -SearchBase ((Get-ADRootDSE).schemaNamingContext)  -SearchScope OneLevel -LDAPFilter "(searchFlags:1.2.840.113556.1.4.803:=32)" -Property objectClass, name, whenChanged,  whenCreated, LDAPDisplayNAme  | Out-GridView  
Write-Host "ANR Enabled Attributes"  
Get-ADObject -SearchBase ((Get-ADRootDSE).schemaNamingContext)  -SearchScope OneLevel -LDAPFilter "(searchFlags:1.2.840.113556.1.4.803:=4)" -Property objectClass, name, whenChanged,  whenCreated, LDAPDisplayNAme | Out-GridView  
Write-Host "Indexed Enabled Attributes"  
Get-ADObject -SearchBase ((Get-ADRootDSE).schemaNamingContext)  -SearchScope OneLevel -LDAPFilter "(searchFlags:1.2.840.113556.1.4.803:=1)" -Property objectClass, name, whenChanged,  whenCreated, LDAPDisplayNAme  | Out-GridView  
  
The above script is something I use to quickly look and see what is indexed in an AD environment

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices