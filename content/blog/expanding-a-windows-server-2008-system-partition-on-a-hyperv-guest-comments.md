---
title: 'Expanding a Windows Server 2008 System partition on a HyperV Guest'
date: 2008-09-02T19:47:00.001-07:00
draft: false
url: /2008/09/expanding-windows-server-2008-system-comments.html
tags: 
- HyperV
- ILM 2 Beta 3
- Windows Server 2008
---

#### Yeah, WOW, not a quick and easy process by any means!
[Brad Turner](https://www.blogger.com/profile/13950085747222995199 "noreply@blogger.com") - <time datetime="2008-09-17T19:08:00.000-07:00">Sep 3, 2008</time>

Yeah, WOW, not a quick and easy process by any means!
<hr />
#### Good Info - Important Note: If you are dealing wit...
[Unknown](https://www.blogger.com/profile/02415410667246276267 "noreply@blogger.com") - <time datetime="2013-10-08T07:00:05.855-07:00">Oct 2, 2013</time>

Good Info - Important Note: If you are dealing with a vm guest attached to a Hyper-V Cluster, You'll need to use Failover Cluster Manager in Administration Tools on one of the Cluster Nodes - After making the change, go to a Command Prompt and enter the following:  
diskpart  
DISKPART> list  
DISKPART> list volume  
DISKPART> select volume #  
DISKPART> extend  
DISKPART> extend filesystem  
You'll need to run extend filesystem on ant 2008+ server regardless if it is in a Cluster or not...
<hr />
