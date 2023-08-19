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

Michael Pearn from down under wrote about his [experience trying to use just Declarative Sync Rules](http://blog.kloud.com.au/2013/10/04/fim-case-study-trying-to-achieve-a-100-declarative-or-codeless-architecture/)

His experience -- especially the religious debates are similar to my own. It made me recall my presentation at TEC 2012 the FIM 2010 R2 Showdown: Classic vs. Declarative

The vast majority of old hands at the presentation declared for Classic both before and after the presentation. During the presentation I attempted to view anything you could do without code as declarative whether it came from a sync rule or not, especially if it was a new feature. But the crowd wouldn't let me claim anything configured in the sync engine as declarative. But in this post only classic code counts as not declarative.

Michael found that he needed classic code for Advance Join rules, doing anything with multi-valued attributes other than just flowing them and "Converting Binary values to ISO8601 Datetime." In his example he could have modified his SQL query that gets the data from HR and avoided the need for the Advanced Join rule.

In addition to Michael's list here are some other things that you may need **classic code** to do:

*   Advanced Filtering scenario to cause disconnections
*   Changing the Metaverse object type when a connector joins to it
*   Join Resolution Rules
*   Manual Precedence Import Flows
*   Provision objects with Auxiliary classes
*   Decide on a case by case basis whether to deprovision as a Disconnector, Explicit Disconnector or just delete the object.

But what does the FIM Sync engine bring us beyond what we had in ILM 2007 FP1?

*   A lot less need for MVDeletion rules extension since we can indicate that disconnection from any of a list of MA's should trigger MV Deletion or if it is disconnected from all MA's (but ignore this one and that one)
*   Many, many attribute transformations can be done with Sync Rules and don't need code
*   A way to do fairly sophisticated provisioning logic without code (Transition Sets, MPRs, Workflows, OutBound Sync Rules)
*   R2: A way to do some basic provisioning logic with filter based Outbound Sync rules that performs pretty decently and doesn't require a detour through the FIM Service
*   New ways to trigger deprovisioning (Transition Sets, MPRs, Workflows, OutBound Sync Rules)
*   OU creation w/o code (That sure is nice and no worried about the OU being a connector to the MV object that first needed it)
*   DN Rename w/o code (also very nice)

In my presentation I contrasted the new sync rules with the classic config and code:

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/762586ead43a_D293/image_thumb.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/762586ead43a_D293/image.png)

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/762586ead43a_D293/image_thumb_3.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/762586ead43a_D293/image_3.png)

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/762586ead43a_D293/image_thumb_4.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/762586ead43a_D293/image_4.png)

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/762586ead43a_D293/image_thumb_5.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/762586ead43a_D293/image_5.png)

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/762586ead43a_D293/image_thumb_6.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/762586ead43a_D293/image_6.png)

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/762586ead43a_D293/image_thumb_7.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/762586ead43a_D293/image_7.png)

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/762586ead43a_D293/image_thumb_8.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/762586ead43a_D293/image_8.png)

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/762586ead43a_D293/image_thumb_9.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/762586ead43a_D293/image_9.png)

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/762586ead43a_D293/image_thumb_10.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/762586ead43a_D293/image_10.png)

Finally here were my recommendations that many disagreed with but it sounds like Michael would agree:

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/762586ead43a_D293/image_thumb_11.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/762586ead43a_D293/image_11.png)

There are some high volume scenarios where sync rules are too slow and there are still some customers that get all they want out the classic sync engine and don't want to pay for CALs.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices