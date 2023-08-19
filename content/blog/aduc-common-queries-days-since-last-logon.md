---
title: 'ADUC Common Queries: Days Since Last Logon'
date: 2014-09-16T12:08:00.001-07:00
draft: false
url: /2014/09/aduc-common-queries-days-since-last.html
tags: 
- AD
---

Recently a client asked me how Active Directory Users and Computers (ADUC) performs the Days Since Last Logon query found in the Find Dialog box's Common Queries option.  
  
LastLogon is not replicated so to really get it you have to query every single DC. So I was reasonably certain that the query didn't use LastLogon but rather used the [LastLogonTimestamp](http://blogs.technet.com/b/askds/archive/2009/04/15/the-lastlogontimestamp-attribute-what-it-was-designed-for-and-how-it-works.aspx) which was created "to help identify inactive computer and user accounts."  Assuming default settings "the _lastLogontimeStamp_ will be 9-14 days behind the current date."  
  
However, I couldn't find any documentation confirming that so I had to test it. For all I knew it could have been querying all the DC's to get an accurate LastLogon.  

  

So when I ran the query yesterday, 15th of Sept, 120 days previous was 5/18 and on the domain controller I was querying the lastlogon of the account in question was 5/20 but the LastLogonTimeStampwas 5/14. So I knew that if the ADUC query showed the account in question that it meant that the ADUC query was using LastLogonTimeStamp because if it was using LastLogon (whether it was querying all of the DC's or just the one) then the account wouldn't show up.  
  
Sure enough the account showed up. Conclusion: ADUC's Days Since Last Logon query is using the LastLogonTimeStamp as I expected.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices