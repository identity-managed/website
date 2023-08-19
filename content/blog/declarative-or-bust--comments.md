---
title: 'Declarative or Bust!'
date: 2013-10-04T15:55:00.001-07:00
draft: false
url: /2013/10/declarative-or-bust.html
tags: 
- Forefront Identity Manager
- FIM 2010 R2
- Identity Management
- FIM
---

#### I see two challenges: 1. There is not feature pari...
[Craig Martin](https://www.blogger.com/profile/09808879680127031778 "noreply@blogger.com") - <time datetime="2013-10-09T10:32:18.412-07:00">Oct 3, 2013</time>

I see two challenges:  
1\. There is not feature parity between the two types of sync rules  
2\. The imperative support (VBA) in the new sync rules is limited and difficult to debug  
  
My wish is that we had better extensibility in the new sync rules (scrap VBA, or figure out how to improve the extensibility and debugging).  
  
Also, choosing between declarative or imperative is a bad choice because you'll always need bits of both. PowerShell is a good example, in the new Desired State Configuration feature:  
http://www.powershellmagazine.com/2013/07/05/imperative-versus-declarative-syntax-in-powershell/
<hr />
#### This is a very technical comparison. Let’s look at...
[Unknown](https://www.blogger.com/profile/10066553024510394551 "noreply@blogger.com") - <time datetime="2014-11-05T10:22:41.643-07:00">Nov 3, 2014</time>

This is a very technical comparison. Let’s look at other arguments.  
• Skilled people for declarative are easier to find. Software writers are scares.  
• The portal knows the sync, but not vice versa. So Understanding the whole logic is much easier when using Declarative.  
• Are we integrators or a software house? We don’t write our own virus scanner, do we?  
• Reporting over Declarative is OOTB. Reporting over Classic is not available.  
• Clients dislike these DLLs where all the “secret stuff” is.  
• While it’s true that classic can do anything, that’s also the problem. If you look at the code you will often find some very creative stuff… I would lough if it wasn’t me.  
• Judging by the development since ILM 2007, the future is Declarative. Who wants to be left behind?
<hr />
#### I think I get your perspective, Guy; you prefer a ...
[Craig Martin](https://www.blogger.com/profile/09808879680127031778 "noreply@blogger.com") - <time datetime="2014-11-06T15:13:22.969-07:00">Nov 4, 2014</time>

I think I get your perspective, Guy; you prefer a system that is easier to build and operate, and your priority is not extensibility. That sounds reasonable, but I think the goals are not exclusive. Maybe someday we'll have both, but in the interim Microsoft agrees with you ;-)
<hr />
