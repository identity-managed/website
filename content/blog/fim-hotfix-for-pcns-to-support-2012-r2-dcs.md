---
title: 'FIM Hotfix for PCNS to support 2012 R2 DC''s'
date: 2015-04-30T13:46:00.000-07:00
draft: false
url: /2015/04/fim-hotfix-for-pcns-to-support-2012-r2.html
tags: 
- FIM 2010 R2
- FIM
---

With the [latest hotfix](https://support.microsoft.com/en-us/kb/3048056) MSFT now supports running PCNS on Windows Server 2012 R2. FIM still should not be installed on Windows Server 2012 R2 (2012 yes, 2008 R2 yes, 2008 yes). Only PCNS can be installed on Windows Server 2012 R2. The hotfix article has a slight error indicating that it is ok to install FIM Sync Service on 2012 R2 if you have installed the hotfix PCNS on 2012 R2 -- not true (the article should get corrected soon). Be warned this update may break ECMA 1 and ECMA 2.0 based MA's. That is they may not run returning "stopped-extension-dll-load" There are workarounds published in the article.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices