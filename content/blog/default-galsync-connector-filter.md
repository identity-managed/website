---
title: 'Default GalSync Connector Filter'
date: 2010-09-07T11:35:00.001-07:00
draft: false
url: /2010/09/default-galsync-connector-filter.html
tags: 
- Forefront Identity Manager
- GalSync
- FIM
---

Using FIM 2010 RTM Update 1:

The default GalSync Connector Filter is to filter out user objects that are hidden from the addressbook, OR missing the legacyExchangeDN, OR missing both the msExchangeHomeServerName and targetAddress are missing, OR proxyAddresses are missing, OR if it is a Mailbox Plan, Arbitration Mailbox, or Discovery Mailbox.

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/DefaultGalSyncConnectorFilter_A2DC/image_thumb.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/DefaultGalSyncConnectorFilter_A2DC/image.png)

Consequently, this answers the question are mail-enabled users filtered out by default?

No they are not, as a mail-enabled user will have the target address populated, and none of the other rules will filter it out.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices