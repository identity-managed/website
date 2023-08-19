---
title: 'Problems with Sync Rules in ILM 2 RC0 (err FIM RC0)?'
date: 2009-04-20T18:08:00.001-07:00
draft: false
url: /2009/04/problems-with-sync-rules-in-ilm-2-rc0.html
tags: 
- Forefront Identity Manager
- FIM
- ILM 2 RC0
---

#### If you will take a look at FIM(ILM) connections sc...
[Unknown](https://www.blogger.com/profile/06128691531408607025 "noreply@blogger.com") - <time datetime="2009-04-21T00:56:00.000-07:00">Apr 2, 2009</time>

If you will take a look at FIM(ILM) connections schema you will see that ILM MA has a direct SQL connectivity to FIM database (not through web service). As far as I know any change to metaverse schema fires up synchronization of this change to FIM database directly through SQL connection.
<hr />
