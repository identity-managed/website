---
title: 'Live ID''s are now Open ID''s, Geneva supports SAML 2.0'
date: 2008-10-30T16:37:00.001-07:00
draft: false
url: /2008/10/live-id-are-now-open-id-geneva-supports.html
tags: 
- ADFS
- AD FS
- Geneva
- Shibboleth
- CardSpace
- Zermat
---

At the [PDC Microsoft's Kim Cameron and colleague Bertocci Vittorio](http://channel9.msdn.com/pdc2008/BB11/) announced that Microsoft Live is now an Open Id provider. Additionally, when signing into Live you can use Information Cards (Info Card, Card Space, Geneva Card Space).

They also demonstrated the new Geneva Framework (formerly known as Zermat) -- essentially a successor to Windows Server 2008 Active Directory Federation Services, and showed it supporting SAML 2.0 the "protocol" not just SAML 2.0 the token.

Other new announcements included the Microsoft Federation Gateway, which allows you to federate with Microsoft,  Live (including both managed domains and individual consumers -- all 400 million of them), other Geneva (ADFS) organizations, and other third party Service Token Services (STS). They also showed issuing LINQ queries against the .Net Access Control Service to retrieve roles to make authorization decisions.

Good show gentlemen! This is a tremendous step forward for interoperability. I just hope that the interoperability between Geneva and other third parties STS's is much easier to implement than the brittle, painful interoperability between [ADFS and Shibboleth](http://blog.identityjunkie.com/2008/01/adfs-and-shibboleth-system-13c.html) (that didn't support SAML 2.0). Hopefully, Shibboleth will be one of those 3rd parties!

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices