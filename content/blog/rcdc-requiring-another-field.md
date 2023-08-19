---
title: 'RCDC Requiring another field'
date: 2011-06-14T20:30:00.001-07:00
draft: false
url: /2011/06/rcdc-requiring-another-field.html
tags: 
- Forefront Identity Manager
- FIM
---

Ok I just had to blog this.

I created a custom resource type in FIM for resource mailboxes (Room and Equipment) with accompanying RCDC’s. Based on a Boolean attribute I [hide or make visible a tab](http://www.identitytrench.com/2010/08/hiding-tabs-in-fim-2010-rcdcs.html) of info about Room resources on the edit and view RCDC’s.  (You can’t do that to the create RCDC because the object doesn’t yet exist)

But, I would like to make room number on the Hidden tab to be required when the tab is visible, and not when the tab isn’t. Obviously I can’t do that on the create because the object doesn’t yet exist and so I can’t reference the Boolean attribute. So I just set the required property to true and figured it would work or not. – It does not work. The tab is still hidden until I click finish and then the tab is revealed and it insists on input to the field “The required field cannot be empty”.

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/97bec363cce2_A0CD/image_thumb.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/97bec363cce2_A0CD/image.png)

Isn’t that just weird?

However, by binding the required property of the control to the same Boolean attribute as the visible property of the tab uses we don’t get the same issue. It keeps the tab hidden when it is not a room, but shows the tab when it is a room and requires those fields.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices