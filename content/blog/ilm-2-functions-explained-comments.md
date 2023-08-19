---
title: 'ILM 2 Functions Explained'
date: 2009-01-06T13:08:00.001-07:00
draft: false
url: /2009/01/ilm-2-functions-explained.html
tags: 
- ILM
- ILM 2 RC0
---

#### Excellent post David, thanks for putting this toge...
[Brad Turner](https://www.blogger.com/profile/13950085747222995199 "noreply@blogger.com") - <time datetime="2009-01-07T15:06:00.000-07:00">Jan 3, 2009</time>

Excellent post David, thanks for putting this together!
<hr />
#### To remove bit #2 shouldn't you use BitAnd(-3,u...
[Isidoro Busdraghi](https://www.blogger.com/profile/04290036938524999018 "noreply@blogger.com") - <time datetime="2009-07-10T05:24:19.781-07:00">Jul 5, 2009</time>

To remove bit #2 shouldn't you use BitAnd(-3,userAccountControl) ?
<hr />
#### Paolo is correct in pointing out that the numbers ...
[David Lundell](https://www.blogger.com/profile/17202883653808140101 "noreply@blogger.com") - <time datetime="2010-06-04T09:54:26.894-07:00">Jun 5, 2010</time>

Paolo is correct in pointing out that the numbers I calculated for masks are wrong. I did 32-bit numbers and tested it back on the 32-bit version of the ILM 2 Beta 3 VM. The calcs should be done using 64-bit as explained here: Using FIM to enable or disable accounts in Active Directory (http://social.technet.microsoft.com/wiki/contents/articles/using-fim-to-enable-or-disable-accounts-in-active-directory.aspx )
<hr />
