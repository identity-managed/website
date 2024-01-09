---
title: 'ILM "2" confirmHumanity="false"'
date: 2008-12-23T12:52:00.001-07:00
draft: false
url: /2008/12/ilm-confirmhumanity-comments.html
tags: 
- ILM
- Humor
- ILM 2 RC0
---

#### With Joe's permissions I am posting the comment he...
[David Lundell](https://www.blogger.com/profile/17202883653808140101 "noreply@blogger.com") - <time datetime="2008-12-31T08:24:00.000-07:00">Dec 3, 2008</time>

With Joe's permissions I am posting the comment he attempted to post earlier:  
Apologies for spoiling the fun, but the confirm humanity config setting has no effect in ILM “2”.  
  
This config setting is leftover from the early days of the product when we included Captcha support for AuthN. Setting this to true meant that users would go through a Captcha gate during AuthN, much like I had to do when submitting a comment. We removed that feature early on in ILM and omitted cleaning up the default config file. Today if you want a Captcha gate you would have to add a custom AuthN workflow.  
  
Hope that helps,  
  
Joe Schulman
<hr />
