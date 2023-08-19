---
title: 'Top 5 Deprecated features as of FIM 2010 R2 SP1'
date: 2013-01-16T11:28:00.001-07:00
draft: false
url: /2013/01/top-5-deprecated-features-as-of-fim.html
tags: 
- Forefront Identity Manager
- FIM 2010 R2
- FIM
---

Yesterday Microsoft published a list of features that have been [deprecated in FIM](http://technet.microsoft.com/en-us/library/jj879229(v=ws.10).aspx) and will be removed from the product at some point in the future. In other words these don't require immediate action but when the next major release of \* Identity Manager (\* because we don't know what the new name will be -- see my tweet from last week at the Redmond Identity Summit) emerges those features will likely be gone. So over the next 18-36 months you need to begin working away from these issues.

Rank

Feature

Impact

1

Combined Run Profiles steps such as Delta Import/Delta Sync, Full Import/Delta Sync, and Full Import/Full Sync

Removing the Delta Import/Delta Sync combined run profile step will have a huge impact on shops that have lots of disconnectors in their connector space. Remember that disconnectors are considered pending and so a delta sync always processes them. The Delta Import/Delta Sync single step only processes pending objects that were imported during the delta import.  
  
Hopefully, MSFT will add a feature: a checkbox to determine whether you want to process all disconnectors or just those with import changes since your last sync.

2

Multi-mastery/equal precedence

As [Paul Loonen describes it](http://social.technet.microsoft.com/Forums/en-US/identitylifecyclemanager/thread/2c4f5c39-de0b-4fed-9cdd-057d0394085b):

As a net effect, when the MV attribute is multi-valued, all values contributed by the different MAs are accumulated in the MV attribute.  
When the MV attribute is single valued, the value that is last contributed is stored in the MV attribute, or, “_the last writer wins_”.

The deprecation article leaves in a bit of confusion it says it will be removed but you can still keep using it if you have the FIM MA deployed:

You can continue to use this feature if your environment has a FIM Service management agent deployed (this management agent does not provide manual precedence) and to avoid export-not-precedent for declarative provisioning.

So will it be removed or not?

3

ECMA1 (XMA)

Lots of XMA (ECMA 1) code running out there and all of it will need to be switched to ECMA 2.0 at some point in the future. While I have this one third this could actually have the biggest impact. If someone could create a tool that would auto-magically transform them that would be cool. I don't expect that they would take advantage of all of the new features but at least people will be able to upgrade without tons of recoding.

4

Transaction properties

This handy feature is used in many advanced coding scenarios to be able to signal to your provisioning code that this object just projected or joined and then to take some one time action or skip taking some action.

5

FIM CM MA and CLMUtils

So unlike the Lotus Notes MA and SAP R/3 MA which have been replaced with newer versions the FIM CM MA doesn't look like it will be getting replaced. Honestly there aren't many implementations using this MA. But this has some portents about the future of FIM Certificate Management. I would say that it suggests no future development of FIM CM but they did just add support for the DataCard CD800 printer as part of SP1 so I don't think it is going away entirely.   At a minimum it does suggest a decoupling of the FIM CM from the rest of FIM.  
  
I do think that the acquisition of PhoneFactor suggests that Smart Cards and certificates will have less importance in the authentication game.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices