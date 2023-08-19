---
title: 'Best Practices ILM 2007 Coding Conventions and Habits'
date: 2009-06-22T15:31:00.001-07:00
draft: false
url: /2009/06/best-practices-ilm-2007-coding.html
tags: 
- ILM
---

#### Thanks for writing this up, David. That's goo...
[matthew gibson](https://www.blogger.com/profile/00592893535303741690 "noreply@blogger.com") - <time datetime="2009-06-23T08:17:27.937-07:00">Jun 2, 2009</time>

Thanks for writing this up, David. That's good information.  
  
Can you explain this point...  
I have seen one developer use the flow rule names as a language to processor module to handle 90% of his string manipulation. That certainly cut down on the need for re-coding.  
  
I'm not sure I follow.  
  
Thanks, Again. Matthew
<hr />
#### One developer wrote a module that could interpret ...
[David Lundell](https://www.blogger.com/profile/17202883653808140101 "noreply@blogger.com") - <time datetime="2009-06-28T23:19:14.261-07:00">Jun 0, 2009</time>

One developer wrote a module that could interpret stuff like this  
Person:SN + "," + GivenName -> User: displayname  
  
Person:Propercase(SN) + "," + Propercase(GivenName) -> User:Displayname  
  
Kind of like codeless provisioning in ILM 2 except that his mechanism for entering the codeless code (grin) was to put it in the flow rule name in Identity Manager so that it would be passed to his code at run time. It was very innovative but confusing as all get out to someone looking at it the first time.
<hr />
