---
title: 'FIM Pitfall for old ILM hands'
date: 2010-03-25T21:40:00.001-07:00
draft: false
url: /2010/03/fim-pitfall-for-old-ilm-hands.html
tags: 
- Forefront Identity Manager
- ILM
- FIM
---

In the days of MIIS 2003 and ILM 2007 we usually wrote our provisioning code to provision a new AD account only when the particular metaverse object didn’t already have any connectors in the AD connector space. With FIM your outbound synchronization rule is quite happy to provision another AD account if the existing one it is joined to doesn’t meet the relationship criteria. So I have usually been in the habit of not worrying about extraneous provisioning if I already had an account connected to that metaverse object.

Well a few days ago I learned that old habits die hard. Fortunately, only 7 duplicate accounts were created and only in the connector space as pending exports of type add. So they were easily dealt with. Nonetheless, it just reminded me that when technology changes sometimes your old instincts can betray you.

One another note: in writing this post I felt a bit like my friend and former co-worker, Craig Martin, who in is very humorous TEC speaker BIO wrote:

> Craig Martin speaks in the third person when writing his own brief biography … spending countless hours weeding out issues in his lab environments learning CLM lessons the hard way in order to beat his chest in triumph and share his scars as lessons in a self-deprecating manner.

Man what a crack up. Of course [his bio](http://www.theexpertsconference.com/us/agenda-speakers/directory-identity-training/speaker-bios/#martin) shows up right after [mine](http://www.theexpertsconference.com/us/agenda-speakers/directory-identity-training/speaker-bios/#lundell) on the [speakers bio page](http://www.theexpertsconference.com/us/agenda-speakers/directory-identity-training/speaker-bios/)! Gosh don’t I feel a bit pompous with the contrast as I list off all of my accomplishments dating back to grade school. Oh, I forgot to mention in my bio that I won 1st place in the Gilroy Unified School District Math Contest when I was in 4th grade! That _treasured_ trophy was kept in a cardboard box for many years until one day my then six year old son asked if I ever earned any trophies – and it has endured several repair jobs since my son got his hands on it. Well I suppose, I just wanted to let people know that I have some [cool things to share this TEC](http://www.ilmbestpractices.com/blog/2010/03/tec-2010-speaking-and-sponsoring.html) and hope you come along to hear them

I also encourage everyone to attend Craig’s session (hopefully he won’t lose his voice this year), of course if you attend [Brad Turner’s session](http://www.theexpertsconference.com/us/agenda-speakers/directory-identity-training/speaker-bios/#turner) right beforehand you won’t even have to change rooms!

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices