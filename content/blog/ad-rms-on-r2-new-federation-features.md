---
title: 'AD RMS on R2 -- new Federation Features'
date: 2009-08-14T21:06:00.001-07:00
draft: false
url: /2009/08/ad-rms-on-r2-new-federation-features.html
tags: 
- AD RMS
- ADFS
- AD FS
- FIM
- RMS
---

AD RMS on Windows Server 2008 R2 adds a really slick feature blogged about here: [Group Expansion for Federated Users](http://blogs.msdn.com/rms/archive/2009/06/09/group-expansion-for-federated-users.aspx "Group Expansion for Federated Users")

Prior to R2 to issue a use license to a federated user they need to specifically be granted permissions. With Windows Server 2008 R2 you can create a contact matching the external federated user and then place the contact in the group and then they have the same RMS permissions as that group.

This is great to be able to include external users in groups, and still without provisioning a user account for them in your domain. Oops, now we need to provision a contact object for them and put that into the group. But perhaps if we combine this capability with custom claims transformation modules to do on demand provisioning the way my coworker [Chris Calderon](http://blog.identityjunkie.com/) demonstrated on Windows Server 2008 at TEC 2009 (to get his slides go to  [http://theexpertscommunity.com/item/show/blog/659/TEC-presentations-now-available](http://theexpertscommunity.com/item/show/blog/659/TEC-presentations-now-available "http://theexpertscommunity.com/item/show/blog/659/TEC-presentations-now-available")  and follow the instructions).

But On-Demand Provisioning only solves half of the battle (and here all of the GI Joe fans thought knowing was half the battle ;)

Even though the user's access has been turned off by their employer disabling or deleting their account, the contact objects on your side still need to get cleaned up. But how to know when to deprovision an account from a federated partner? Perhaps you could use the RMS logging database as a starting point and look for users that haven't accessed the system in a while, email them and see if you get a bounce. After receiving an NDR for a federated user that hasn't accessed anything for months would be a pretty safe bet to delete their contact object.

How to make that happen? Create your own service or scripts to automate querying the logging database and sending the email. Another script to check for NDRs and then write to a table the contacts to be deleted. Then use FIM to read the table and delete the contacts, or your script could do it directly, as appropriate.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices