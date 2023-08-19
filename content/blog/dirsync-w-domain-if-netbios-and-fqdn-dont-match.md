---
title: 'DirSync w/ domain if NetBios and FQDN don''t match'
date: 2013-10-04T16:14:00.001-07:00
draft: false
url: /2013/10/dirsync-w-domain-if-netbios-and-fqdn.html
tags: 
- Forefront Identity Manager
- FIM 2010 R2
- FIM
---

If one of your AD domains has a NetBios domain name that doesn't match the leftmost part of your FQDN you need to have the Replicating Directory Changes permission given to your AD MA account. This is documented in a few places including my book. However, DirSync misses this step. Normally, Dirsync does a very good job of installing and configuring everything which you need without needing you to be an expert in FIM, but this is one thing it misses.

For Example if the FQDN is Exchange.loc but the netbios name of the domain was Snappy then you would use this command to solve the issue

DSACLS "CN=Configuration,dc=exchange,dc=loc" /G "exchange\\Grp\_DirChanges:CA;Replicating Directory Changes;"

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices