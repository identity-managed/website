---
title: 'Answering my FIM RC 1 question'
date: 2009-11-24T09:58:00.001-07:00
draft: false
url: /2009/11/answering-my-fim-rc-1-question.html
tags: 
- Forefront Identity Manager
- ILM
- Identity Management
- FIM
---

Thanks to [Darryl Russi](http://blogs.msdn.com/darrylru/default.aspx) for answering my questions in my earlier post [An Update to FIM RC1](http://www.ilmbestpractices.com/blog/2009/11/update-to-fim-rc1.html "An Update to FIM RC1") where I was asked about something I had read in the release notes:

Some of those items raise a few questions, like how to setup a FIM service that only takes requests from the sync service? Do we setup multiple FIM Service instances and then configure the FIM MA to talk to one of them, and not make that one available to web clients?

So the short answer to my last question is yes and then Darryl answers the first question in great deal.

Here is his answer: [Service Partitions - Multiple Middle Tiers, Request & Workflow Processing](http://blogs.msdn.com/darrylru/archive/2009/11/23/service-partitions-multiple-middle-tiers-request-workflow-processing.aspx "Service Partitions - Multiple Middle Tiers, Request & Workflow Processing")

Great job Darryl! I see this as a great way to ensure good response time for users and to scale out.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices