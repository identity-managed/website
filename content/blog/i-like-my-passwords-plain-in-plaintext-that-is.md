---
title: 'I like my passwords Plain --in plaintext that is'
date: 2008-07-03T16:32:00.003-07:00
draft: false
url: /2008/07/i-like-my-passwords-plain-in-plaintext.html
tags: 
- ILM 2 Beta 3
---

[![](http://www.ilmbestpractices.com/blog/uploaded_images/PlainPasswords_small-736256.jpg)](http://www.ilmbestpractices.com/blog/uploaded_images/PlainPasswords_small-736260.jpg)  

Bug in ILM2 Beta 3 -- go vote on MSConnect to register your taste!

  

Look for Bug ID 354953

  

**Do you like your passwords plain or with encrypted butter?**

  
As for me and my house we will choose the encrypted butter! I mean passwords.

ILM 2 codeless provisioning looks great! You can add complex rules without code and then you can even see these rules as they get synchronized into the ILM synch engine (what we know and love from the MIIS 2003 and ILM 2007 days). But then oops! you can see my default password in plaintext!  

  
7/3/2008

In the ILM2 Portal when I configure an initial outbound attribute flow for unicodepwd (an initial password for AD users) and then in Identity Manager looking at the resulting Synchronization rule object in the connector space I can see the password in plaintext!  
Repro Steps  
1) Assume use of VPC image from ILM product group2) Open Identity Manager3) Search the ILM 2 MA connector space -- look for the synchronization rule for provisioning users in my system the id begins with 102df8d94) Click on the elipsis button in the string column of the initial flow attribute then look for Pass@word15) Realize that your password is stored in plaintext!

  
Bigger screenshot of Identity Manager here:

  

![](http://www.ilmbestpractices.com/blog/uploaded_images/PlainPasswords-735226.jpg)  
  

  
  
  

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices