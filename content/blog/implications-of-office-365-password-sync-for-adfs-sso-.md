---
title: 'Implications of Office 365 Password Sync for ADFS (SSO)'
date: 2013-06-26T07:18:00.001-07:00
draft: false
url: /2013/06/implications-of-office-365-password.html
tags: 
- ADFS
- Office365
- SSO
---

[The article on Password Sync for Office 365](http://technet.microsoft.com/en-us/library/dn246918.aspx) is interesting news and clearly states that Federated users can't have their password's synced. In the Community Additions many curious users asked their questions treating it as a forum. Well here are my responses:

If you do Password Sync do you still need ADFS or any other SSO tool that works with Office365? 

Password Sync gives you the ability to login to Office365 using the same username and password that you use with your Active Directory. This is usually referred to as Simplified SignOn or Reduced SignOn. 

ADFS gives you Single Sign On, meaning that when you are on a computer and have already authenticated an SSO token (a SAML token) is stored on your computer and when you access Office 365 services your computer will transmit the token to the Office365 service, which means that you usually won't need to type in your username and password. That is Single Sign On (you signed on a single time and can now access many services).

Does this mean that you don't need ADFS? That depends (the consulting guild requires that I initially answer all questions in that fashion ;). As you can see Password Sync gets you some benefits that previously required ADFS (use the same password as AD) but not all of the benefits (sign in a single time, and not have to re-authenticate to every service).

If your only online service is Office365 and you are willing to live with your users having to type in their passwords repeatedly then you probably don't need ADFS.

If your only online service is Office365 and you do not want your users to have to type in their passwords repeatedly then you do need ADFS.

If you have multiple online services then you want ADFS or another SSO tool so that you can do SSO to all of them (Dir Sync won't sync your password to anything but Office365 and its Azure AD).

Another question asked is about Password Reset -- in effect why does the Office365 Password Reset feature get disabled if you do Password Sync? The answer is that if you are syncing passwords your local AD is now in charge of passwords (good because it simplifies things for the users -- fewer passwords to remember) rather than Office 365. I suppose Microsoft could have set it up whereby the password reset tool would reset the on premise AD password but probably felt that was too invasive and risky. So if you do go with Password Sync users need to reset their passwords in the local AD using whatever means you already have to do that -- Forefront Identity Manager, some third party Password Reset tool, or the helpdesk.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices