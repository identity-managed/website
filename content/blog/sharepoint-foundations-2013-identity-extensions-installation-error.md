---
title: 'SharePoint Foundations 2013 -- Identity Extensions Installation error'
date: 2018-03-29T16:09:00.000-07:00
draft: false
url: /2018/03/sharepoint-foundations-2013-identity.html
tags: 
- #MIM
- #SharePoint
---

As you install SharePoint 2013 Foundations pre-reqs if you encounter "Microsoft Identity Extensions Installation error"  

[![](https://4.bp.blogspot.com/-tYOhqyY_mCE/Wr1ysErFnjI/AAAAAAAAAKk/SxiqPGtc4AIgaUt6dgPO-rdlk4_6CpVWgCLcBGAs/s320/Identity%2BExtensions%2BError.png)](https://4.bp.blogspot.com/-tYOhqyY_mCE/Wr1ysErFnjI/AAAAAAAAAKk/SxiqPGtc4AIgaUt6dgPO-rdlk4_6CpVWgCLcBGAs/s1600/Identity%2BExtensions%2BError.png)

and then when you install it manually you might encounter  
"Installation of Microsoft Identity Extensions requires Windows Identity Foundation v1.0 to be installed"  

[![](https://1.bp.blogspot.com/-3aPHBXaDdq8/Wr1zJ3kOV8I/AAAAAAAAAKo/vGKk33EMbFQHcLwwCnTV4AkpJMnk13oPwCLcBGAs/s320/Identity%2BFoundation%2BRequired.png)](https://1.bp.blogspot.com/-3aPHBXaDdq8/Wr1zJ3kOV8I/AAAAAAAAAKo/vGKk33EMbFQHcLwwCnTV4AkpJMnk13oPwCLcBGAs/s1600/Identity%2BFoundation%2BRequired.png)

  

[![](https://3.bp.blogspot.com/-ZiPEE93Hcdw/Wr1zJ9WqB2I/AAAAAAAAAKs/iu_QHJbxy7wO46i8v_y1jjnr2CkMiedqQCLcBGAs/s320/WIF%2B3_5.png)](https://3.bp.blogspot.com/-ZiPEE93Hcdw/Wr1zJ9WqB2I/AAAAAAAAAKs/iu_QHJbxy7wO46i8v_y1jjnr2CkMiedqQCLcBGAs/s1600/WIF%2B3_5.png)

Then when you go to install WIF through the Server Manager you realize that it is WIF 3.5 rather than WIF 1.0 and you think hmm... maybe that will work. It will. Take heart.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices