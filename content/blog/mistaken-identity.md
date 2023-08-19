---
title: 'Mistaken Identity'
date: 2014-10-03T12:03:00.000-07:00
draft: false
url: /2014/10/mistaken-identity.html
tags: 
- Forefront Identity Manager
- MIIs
- Humor
- Identity Management
- FIM
---

Years ago, I walked into the client site a few months into an Identity Management project, and the PM told me his account had been deactivated by mistake as an employee with the same last name and same first initial was terminated, and they termed his account by mistake.  
  
Ironic.  
  
A few years before that I visited a client whose VP of HR had his account disabled when they let the janitor go. Again same last name but this time the same first name.  
  
What went wrong?  
  
In both cases the AD account was linked to the wrong employee record.  
  
How did that happen?  
  
In the first example they had been diligently entering the employeeID into the employeeID field in AD long before Identity Management. The helpdesk had a tool to query the HR database to look up an employee ID. Apparently, the day this PM had been hired HR was a little slow or the helpdesk made a mistake. Either way they plugged in the wrong employeeID into his AD account. So when the other gentleman was termed, the script they ran (this was before we turned on FIM) disabled his account too.  
  
Garbage in, garbage out. While FIM was not the "perpetrator" it would have done the same thing acting on the wrong data.  
  
In the HR of VP example, the initially joining was done using MIIS (a FIM predecessor) based on first name and last name. Somehow in the intervening years no one noticed that the wrong job title had been pushed into AD.  
  
So how can you avoid this? You can't entirely, but you can reduce the # of occurrences. The first step is to understand the data you are given. The second step is to question the validity of the data -- especially if a human was involved. If the whole process has been automated then any errors should be consistent throughout. A firm hiring George Cludgy (instead of Clooney) would have that data flow from HR out to AD and everywhere else with the correct employeeID. The name itself might be wrong but at least it would be consistent. However, if a human gets involved to do data entry, even though the look it up you have a chance for errors. So you can't take the presence of an employeeID in AD for granted. You must question its validity and confirm it.  
  
I prefer to get dumps of HR and AD and use PowerShell to match them up. Just kidding, this is a job for SQL. While PowerShell actually can do some matching this really is a job for SQL.  
  
By then running queries in my database before setting up FIM I can get a good idea of the matches and non-matches. I can then get the client to confirm the matches and fix the non-matches.  
  
Steps:  
1) Look at and understand the data  
2) Question its validity  
   Did humans input the data?  
3) Export from AD using csvde  
4) Get an export of the employees  
5) Load 3 and 4 into a SQL database  
6) write some queries joining based on employeeID (if present)  
7) look at the matches and come up with some additional ways to verify such as including First name and last name  
8) use a nick name database to handle the David vs Dave issues.  
9) Use Fuzzy lookups from SSIS to generate possible matches.  
10) Get the client to validate your matches, especially the possible matches  
11) Get the client to work on the non-matches (these accounts may end up getting disabled if no match can be found)

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices