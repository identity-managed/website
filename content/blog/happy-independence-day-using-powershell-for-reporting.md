---
title: 'Happy Independence Day -- Using PowerShell for Reporting'
date: 2014-07-04T15:06:00.002-07:00
draft: false
url: /2014/07/happy-independence-day-using-powershell.html
tags: 
- PowerShell
- Reporting
- AD
---

Unfortunately, my Independence day is not free -- I am working. Just so happens I need to report on when computer objects are getting migrated to a new AD forest. Day 1 4 Day 2 30 Day 3 25 etc.  
  
Now I could have taken the data and imported it into SQL and then busted out some awesome queries in no time flat. But my buddy Craig Martin, keeps insisting how awesome this PowerShell stuff is. So I decided to give it a try, plus if I can get it to work then it will be faster to run this repeatedly from PowerShell rather than needing to import it into SQL Server. I am actually a big believer in using the right tool for the job. Otherwise you end up blaming the tool for failing you when you should have picked a different tool, one better suited for your task.  
  
When working in a language of which I am not yet the master, I like to start small and build, so that I don't create 15 billion places to troubleshoot my code. So we start with using Get-ADComputer. Made certain that my filter, searchbase, searchscope and properties give me what I want:  
  
 Get-ADComputer -filter \* -searchscope subtree -SearchBase "OU=Workstations,DC=Domain,dc=com" -Resultsetsize 4000 -Properties **whenCreated**  
  
whenCreated gives me the complete date and time but I want to group and count by day. So I needed to transform the whenCreated to date with no time. The .Date method will work for that but I struggled with how to get it into the pipeline for further processing. Eventually I discovered that I can use the @ symbol to note a hash table and tell the Select-Object commandlet to transform it with an expression and give the result a new name. (Thanks [Don Jones](http://technet.microsoft.com/en-us/magazine/ff394367.aspx))  
 Get-ADComputer -filter \* -searchscope subtree -SearchBase "OU=Workstations,DC=Domain,dc=com" -Resultsetsize 4000 -Properties whencreated  | Select-Object -Property Name,@{Name="DateCreated"; Expression = {$\_.WhenCreated.Date}}   
  
 I later [discovered I could do the same thing with the Group-Object commandlet](http://windowsitpro.com/powershell/exploring-powershells-group-object-cmdlet) which simplifies the command set. So I tack on:  | Group-Object  @{Expression = {$\_.WhenCreated.Date}}  -NoElement   
to get:  
  
 Get-ADComputer -filter \* -searchscope subtree -SearchBase "OU=Workstations,DC=Domain,dc=com" -Resultsetsize 4000 -Properties **whenCreated** | Group-Object  @{Expression = {$\_.WhenCreated.Date}}  -NoElement   
  
But then in sorting it if I want to get a true sorting by date rather than a textual sorting I once again need to do an expression because the Group-Object commandlet has transformed my DateTime values into strings so I tack on:  
| Sort-Object @{Expression = {\[datetime\]::Parse($\_.Name) }}  
  
So all together with a little message at the beginning:  
Write-host "Daily totals of computer migrations"  
Get-ADComputer -filter \* -searchscope subtree -SearchBase "OU=Workstations,DC=Domain,dc=com" -Resultsetsize 4000 -Properties whencreated  | Group-Object  @{Expression = {$\_.WhenCreated.Date}}  -NoElement | Sort-Object @{Expression = {\[datetime\]::Parse($\_.Name) }}  

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices