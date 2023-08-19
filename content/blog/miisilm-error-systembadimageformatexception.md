---
title: 'MIIS/ILM Error: System.BadImageFormatException'
date: 2008-08-20T17:08:00.001-07:00
draft: false
url: /2008/08/miisilm-error-systembadimageformatexcep.html
tags: 
- MIIs
- ILM
---

So I had MIIS 2003 SP 1 reporting to me that the format of my GalSync-Extension.dll is invalid. So I tried recompiling it -- no luck. Same error. The only [MSDN article](http://msdn.microsoft.com/en-us/library/k7137bfe(VS.80).aspx) on this indicated that unmanaged code is being passed to the load method.

Through trial and error we found the solution: stop and start the MicrosoftIdentityIntegrationService. If that doesn't work try a reboot.

[![BadImageFormatException_screenshot](http://www.ilmbestpractices.com/blog/uploaded_images/WeirdMIISILMerroranditsresolution_AAE7/BadImageFormatException_screenshot_thumb.png)](http://www.ilmbestpractices.com/blog/uploaded_images/WeirdMIISILMerroranditsresolution_AAE7/BadImageFormatException_screenshot.png)

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices