---
title: 'The Grand Unified Demo of Identity Management'
date: 2008-05-07T13:57:00.002-07:00
draft: false
url: /2008/05/grand-unified-demo-of-identity.html
tags: 
- MIIs
- ILM
- ADFS
- AD FS
- Identity Management
- CLM
- RMS
---

As I was architecting and assembling the Identity All Up workshop (part of the 2008 Directory Experts Conference see the [review by Felix Gaehtgens, an analyst for Kuppinger Cole](http://blogs.kuppingercole.com/gaehtgens/2008/03/03/netpro-dec-2008-sneak-preview-of-microsoft-ilm-2/)) designed to expose the attendees (or delegates) to all facets of the Microsoft Identity Access Platform, Lori Craw, from Microsoft referred to this as the "Grand Unified Demo". I chuckled, instantly catching the reference to the still undiscovered Grand Unified Field theory that eluded Einstein and even today's theoretical physicists.  
  
In creating and delivering this workshop, I have reinforced, my earlier belief that the Active Directory (AD) is the medium through which most of these interactions happen that allow for interactions between these components of the platform, and Identity Lifecycle Manager (ILM) is the driving force.  
  
Allow me to explain -- In order to manage the lifecycle of smart cards through Certificate Lifecycle Manager (CLM) you must belong to groups in AD that have been assigned permissions to the CLM Service Connection Point, the CLM Profile Template, the CLM Certificate Template, and a group that contains the user upon whom you will act. How do you get into these groups? Through Identity Lifecycle Manager! So AD is the medium and ILM the driver.  
  
In the case of CLM, ILM also has a more direct connection through the Certificate Lifecycle Management agent through which ILM can provision, enroll requests, termination requests, suspend requests, renewal requests, and unblock requests.  
  
Let's take a look at Active Directory Rights Management Services (RMS). With RMS permissions as with most other permissions, they are assigned to Groups in AD. Once more -- AD is the medium and ILM is the driver.  
  
Now please turn your attention to Active Directory Federated Services (AD FS). Users get access to resources at the resource partner by virtue of having claim that gives them access, most of the time this claim will be a group claim. Once more -- ILM is driving through the medium of AD.  
  
Even more, look at AD RMS integration with AD FS. Now we can extend Rights Management protection to documents while sharing them with partners without the unrealistic expectation for the partner to have their own AD RMS infrastructure (the requirement for RMS prior to Windows Server 2008). Once more, access for partners is through being member of a group that establishes an outgoing claim to the resource partner that is then consumed by RMS, and once more the best way to get users into groups is through ILM.  
  
Expand your horizons, once more, now using a smart card (provisioned through an ILM request to CLM), we can authenticate to the Directory build the list of groups to which we belong (managed by ILM), we can access an RMS protected document at a Partner's SharePoint site, and have the appropriate restrictions apply to us.  
  
Wait, what about AD Lightweight Directory Services (AD LDS -- formerly known as ADAM), and Windows Cardspace? Where do they fit in?  
  
AD LDS can be used as another repository for storing identities usually for your extranet, for partners that aren't federation ready (either because of lack of size, technology, or policy). AD FS can use AD LDS as one of its account stores! Hence the same protection of RMS documents can be extended once more to non-federation partners without the need for another RMS infrastructure -- in fact vendors could offer RMS as a service using ADFS and AD LDS to cover the authentication needs.  
  
What about Card Space? Card Space, can also be incorporated, but that is a topic for another day.  
  
I want to give special thanks to Chris Calderon for his tireless efforts in helping me setup the virtual machines and hammering out the AD RMS AD FS integration with Sharepoint. Thanks also to David Wozny (pronounced Wahznee) for improving and delivering the deepdive into CLM. Thanks to Craig Martin for assisting David Wozny in improving the ILM deepdive. Additional thanks to Bob Tucker for helping with the VM setup. Thanks to Hugh Simpson-Wells and James Cowling for editing the labs. Thanks to James Booth for listening and improving while I dreamed up the scenarios used in the labs.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices