---
title: 'SharePoint Foundation 2013 IIS Configuration Error'
date: 2018-03-29T15:54:00.000-07:00
draft: false
url: /2018/03/sharepoint-foundation-2013-iis.html
tags: 
- MIM
- #FIM
- #MIM
- #SharePoint
- FIM
---

SharePoint is a great product but I wish that FIM and MIM did not use it. In my opinion, it adds unnecessary infrastructure and really complicates the setup, because SharePoint must be installed and configured (and maintained). Leaving that aside, allow me to point out some gotchas that might impede your ability to install this MIM/FIM prerequisite.  
  
First up: if your server has limited access to the Internet you should probably download all of these prerequisites and copy them to the server -- because that's what the SharePoint Installer has to do -- it doesn't include these items.  
  
Should you encounter the following message:  
Application Server Role, Web Server (IIS) Role: configuration error  

[![](https://4.bp.blogspot.com/-BFFlwi_7hVM/Wr1sDuGgtjI/AAAAAAAAAJ4/JTIiRG-qScU5mNceggksHowmGjeOQ7H0wCLcBGAs/s320/SharePointFoundation2013_error_IIS_Role_Configuration_error.png)](https://4.bp.blogspot.com/-BFFlwi_7hVM/Wr1sDuGgtjI/AAAAAAAAAJ4/JTIiRG-qScU5mNceggksHowmGjeOQ7H0wCLcBGAs/s1600/SharePointFoundation2013_error_IIS_Role_Configuration_error.png)

If you click on Review the Log File and find this:  
  

 - "C:\\WINDOWS\\system32\\cscript.exe" "C:\\WINDOWS\\system32\\iisext.vbs" /enext "ASP.NET v4.0.30319"

 - Install process returned (1)

\- \[In HRESULT format\] (-2147024895)

  

 - Error when enabling ASP.NET v4.0.30319

  

Then the issue is you are missing some of the IIS Role Services -- specifically the IIS 6 Scripting Tools:

[![](https://1.bp.blogspot.com/-zo5hHcJLvN4/Wr1uPsImqdI/AAAAAAAAAKI/4OLKhqt3MjIMVhgk5m852MMpyyUVKiEaACLcBGAs/s320/IIS%2BRole%2BServices%2BIIS6.png)](https://1.bp.blogspot.com/-zo5hHcJLvN4/Wr1uPsImqdI/AAAAAAAAAKI/4OLKhqt3MjIMVhgk5m852MMpyyUVKiEaACLcBGAs/s1600/IIS%2BRole%2BServices%2BIIS6.png)

Yes this is a screenshot from my book. Yes, I clearly identify that you need these role services. So I must have made this mistake just out of the goodness of my heart in order to help anyone else.

  

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices