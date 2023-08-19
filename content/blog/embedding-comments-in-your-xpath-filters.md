---
title: 'Embedding comments in your XPATH Filters'
date: 2010-07-20T13:22:00.001-07:00
draft: false
url: /2010/07/embedding-comments-in-your-xpath.html
tags: 
- Forefront Identity Manager
- XPATH
- FIM
---

One thing I love to do is provide self-documenting code and configurations. Well when I have to customize sets the XPATH filter can get a bit complex so I recently found a way to comment the XPATH Filter in my sets and groups:

/Person\[starts-with(DisplayName,'%')\] <!-- Only with DisplayName --> </Filter>

By using <!--  --> to enclose my comments and only after the last closing \] of the predicate I can comment on the filter itself.

The following will error (don’t put the comment inside the predicate \[\].

/Person\[starts-with(DisplayName,'%') <!-- Only with DisplayName -–> \]</Filter>

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices