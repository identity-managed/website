---
title: 'Designing and Implementing RBAC Solutions with FIM 2010 Group Management'
date: 2011-04-18T16:33:00.001-07:00
draft: false
url: /2011/04/designing-and-implementing-rbac.html
tags: 
- Forefront Identity Manager
- RBAC
- Identity Management
- TEC
- FIM
- #TEC2011
---

After I introduced Brad Turner and turned the time over to him, he showed off some really cool FIM extensions to enable RBAC. He even showed how it fits the NIST RBAC definitions even through level 3.

The key design decision was to extend the Set and Group objects. The Set then functions as a role. This allows for both explicit and criteria based membership. A new object type for a Role Membership allows for the user’s membership in a role to expire at an individual time.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices