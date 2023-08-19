---
title: 'SharePoint 2010 User Profile Synchronization Service'
date: 2012-05-01T01:52:00.001-07:00
draft: false
url: /2012/05/sharepoint-2010-user-profile.html
tags: 
- Forefront Identity Manager
- FIM
- SharePoint
---

The SharePoint 2010 User Profile Synchronization Service is really FIM 2010 pre-packaged in a very special way. Need evidence? Look at the tables in User Profile Service Application\_SyncDB

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/SharePoint-2010-User-Profile-Synchroniza_196F/image_thumb.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/SharePoint-2010-User-Profile-Synchroniza_196F/image.png)

See how it has mms\_connectorspace, mms\_cs\_link etc. Those are table commonly found in the FIM sync database. See the attributeInternal, the BindingInternal, all of the Membership\* tables those are all part of the FIM Service database. So interestingly enough they have both FIM Service and FIM sync merged into a single DB.

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/SharePoint-2010-User-Profile-Synchroniza_196F/image_thumb_3.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/SharePoint-2010-User-Profile-Synchroniza_196F/image_3.png)

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices