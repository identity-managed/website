---
title: 'Windows 2012 R2 and Windows 8.1 RTM now on MSDN and Technet'
date: 2013-09-11T13:11:00.001-07:00
draft: false
url: /2013/09/windows-2012-r2-and-windows-81-rtm-now.html
tags: 
- Windows Server 2012 R2
- AD FS
- AD
---

One of my fellow MVPs and Insight teammates Alessandro Cardoso (he runs one of our practices down under) announced on his blog that [Windows 2012 R2 and Windows 8.1 RTM now on MSDN and Technet](http://cloudtidings.com/2013/09/10/windows-2012-r2-and-windows-8-1-released-to-msdn-and-technet-subscriptions/#!).

He goes on to mention the salient points around 2012 R2 for virtualization so I thought I would discuss some of the benefits for [Active Directory and ADFS](http://technet.microsoft.com/en-us/library/dn268294(v=ws.11))

One key thing is that ADFS on Windows Server 2012 R2 doesn't require IIS so now it can and should be installed on domain controllers.

But the most exciting aspect is the enhancement to security specifically mobile security. With the advent of [Workplace Join (or Join to Workplace)](http://technet.microsoft.com/en-us/library/dn280945) mobile devices (iOS and Windows) can be part of the domain and participate in SSO.

One of the best enhancements to ADFS is the ability to "Set \[multi-factor authentication\] requirement for all extranet access or conditionally based on the user’s identity, network location or a device that is used to access protected resources." [http://technet.microsoft.com/en-us/library/dn280949.aspx](http://technet.microsoft.com/en-us/library/dn280949.aspx "http://technet.microsoft.com/en-us/library/dn280949.aspx")

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices