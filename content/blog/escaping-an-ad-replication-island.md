---
title: 'Escaping an AD Replication Island'
date: 2015-03-07T09:07:00.001-07:00
draft: false
url: /2015/03/escaping-ad-replication-island.html
tags: 
- Windows Server 2003
- AD
- Windows Server 2008
---

On a dark and stormy night an Active Directory upgrade was underway, Windows Server 2003 domain controllers decommissioned, consolidated and replaced with Window Server 2008 R2 servers. Suddenly I got a call from those doing the upgrade, "I can't see some of the new domain controllers on the existing domain controllers, what's wrong?"  
  
A replication island had been created and several domain controllers were trapped on it. Could we rescue them in time?  
  
[Normally AD automatically generates the replication topology.](http://social.technet.microsoft.com/wiki/contents/articles/4592.how-active-directory-replication-works.aspx) But if you turn that off then you must manually create connection objects between domain controllers. Even if that is enabled replication between sites does require site link objects to be created.  
  
With the sites and site links in place and the Knowledge Consistency Checker (KCC) enabled for generating connection objects, the KCC will automatically generate connection objects between Domain Controllers in different sites (those servers are referred to as Bridgehead servers).  By default all site links are transitive. However, this is often turned off if some sites can't connect to others (routing or firewall configurations may be the cause, but it may be legit). However, site links still need to exist.  
  
In this scenario they had the KCC enabled but site link transitivity was off. As domain controllers in several sites were decommissioned leaving some of the new sites with new domain controllers but without direct site links to sites that still had active domain controllers. As I mapped out the new topology I realized that an island had been created -- four of the new sites could talk to each other but not to the other 20 sites.  
  
**How to get off of the replication island?**  
  
**Create Site links to connect the sites to each other!**   
  
But when you create a site link it exists on that domain controller and needs to replicate to the other domain controllers. So how to get it to replicate when you need site links to replicate?   Talk about your chicken and egg problem!  
  
RepAdmin to the rescue! With [repadmin /replsingleobj](https://technet.microsoft.com/en-us/library/cc742123.aspx) you can force the replication of a single object to any other domain controller even if they aren't replication partners. So after creating the new site links I needed on one of the island domain controllers --  I forced replication among the domain controllers on the island so they all new about the new site link. But the rest of the enterprise still doesn't know so I ran repadmin /replsingleobj NonIslandDC IslandDC "CN=NewIPSITELINK,CN=IP,CN=Inter-Site Transports,CN=Sites,CN=Configuration,DC=MyDomain,DC=rootdomain"  
  
Then I forced the replication from that domain controller to its partners and then forced the KCC to generate a new replication topology. The island was bridged.  
  
**The domain controllers were rescued!**

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices