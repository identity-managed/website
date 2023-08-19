---
title: 'FIM DB Sizing Calculator'
date: 2012-04-25T23:32:00.001-07:00
draft: false
url: /2012/04/fim-db-sizing-calculator.html
tags: 
- SQL
- Forefront Identity Manager
- FIM
---

FIM has two databases (well three if we count the FIM Certificate Management service):

*   FIMService
*   FIMSynchronizationService

[Here is a calculator in excel](http://www.ilmbestpractices.com/files/FIM%20DB%20Sizing.xlsx) that you can download and use to calculate how big to make your databases.

In my experience the FIMService database size depends mostly on how many request objects are in the database.

The FIM Sync Database depends mostly on how much run history details (step object details) you generate and keep.

Let me know how you like it. Remember this is to give you a range and help you with your first order approximation. I tried to carefully spell out all of my assumptions (even taking a Goldilocks approach with High, Low and Probable assumptions) and make them accessible in separate cells, while still trying to preserve the simplicity of how many users, how many groups, how many MA’s dealing with each.

I have tried to make it accurate to my experience. However if you find an outright error or find that it doesn’t match your existing setup let me know.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices