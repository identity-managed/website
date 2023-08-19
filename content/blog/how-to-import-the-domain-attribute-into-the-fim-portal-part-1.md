---
title: 'How to import the Domain attribute into the FIM Portal Part 1'
date: 2012-08-16T12:47:00.001-07:00
draft: false
url: /2012/08/how-to-import-domain-attribute-into-fim.html
tags: 
- Forefront Identity Manager
- FIM 2010 R2
- FIM
---

If you have a single domain forest then you should use a constant flow in your sync rule or advanced attribute flow. If you have a multi-domain forest, then using a constant in the advanced attribute flow won’t work.

You could create multiple inbound sync rules one for each domain with scoping filters and then use a constant. However, this seems like a waste.

You could also follow the guidance provided in article originated by my friend [Markus Vilcinskas](http://social.technet.microsoft.com/wiki/2315/ProfileUrlRedirect.ashx) and maintained by the community [http://social.technet.microsoft.com/wiki/contents/articles/648.how-do-i-synchronize-users-from-active-directory-domain-services-to-fim.aspx](http://social.technet.microsoft.com/wiki/contents/articles/648.how-do-i-synchronize-users-from-active-directory-domain-services-to-fim.aspx "http://social.technet.microsoft.com/wiki/contents/articles/648.how-do-i-synchronize-users-from-active-directory-domain-services-to-fim.aspx")

Which for one domain looks like this:

IIF(Eq(Left(ConvertSidToString(objectSid),41),"S-1-5-21-4220550486-1538840966-3184992408"),"FABRIKAM","Unknown")

and for three looks like:

IIF(Eq(Left(ConvertSidToString(objectSid),41),"S-1-5-21-4220550486-1538840966-3184992408"),"FABRIKAM",IIF(Eq(Left(ConvertSidToString(objectSid),41),"S-1-5-21-4220550586-1538840966-3184992408"),"SnappySlackers",IIF(Eq(Left(ConvertSidToString(objectSid),41),"S-1-5-21-4220550486-1538840966-3184992408"),"bluesky","Unknown")))

However it requires ferreting out the SIDs of the domains (although Markus does provide a script to generate the expression [http://social.technet.microsoft.com/Forums/en-US/ilm2/thread/50088024-d86a-49dc-bb03-3243ebd677eb](http://social.technet.microsoft.com/Forums/en-US/ilm2/thread/50088024-d86a-49dc-bb03-3243ebd677eb "http://social.technet.microsoft.com/Forums/en-US/ilm2/thread/50088024-d86a-49dc-bb03-3243ebd677eb") ). This technique uses the fact that the first 41 characters of the SID (after converting it to a string) of every object is the domain SID.

As you can see the custom expression gets very unwieldy, very fast. In [Part 2](http://blog.ilmbestpractices.com/2012/08/how-to-import-domain-attribute-into-fim_16.html) I shall propose a more elegant solution that works in all cases with one notable exception, that can be worked around.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices