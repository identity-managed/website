---
title: 'Behind the scenes of RoomResources–Custom Properties'
date: 2011-05-16T22:26:00.001-07:00
draft: false
url: /2011/05/behind-scenes-of-roomresourcescustom.html
tags: 
- Exchange 2010
- PowerShell
- FIM
---

While using FIM and PowerShell to manage Exchange 2010 I was following along a [wonderful article on resource mailboxes](http://www.msexchange.org/articles_tutorials/exchange-server-2010/management-administration/resource-mailboxes-exchange-2010-part2.html) that left me wondering a few things.

1) Exactly how is the data stored in the msExchResourceDisplay and msExchResourceSearchProperties attributes?

2) How is it stored with multiple custom properties?

3) Is manipulating those AD attributes sufficient or is PowerShell storing something in the Exchange Data store?

Here are the answers:

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image_thumb.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image.png)

1) msExchResourceDisplay = “Room,FlatScreenTV” It appears to be a single valued string with commas.

msExchResourceSearchProperties at first blush appears to be a single-valued string with semi-colons, however further examination reveals it to be a multi-valued attribute

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image_thumb_3.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image_3.png)

2) What happens when multiple Resource Custom Properties are set?

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image_thumb_4.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image_4.png)

msExchResourceDisplay = “Room,FlatScreenTV,Whiteboard”

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image_thumb_5.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image_5.png)

So the new value is simply added to the old ones.

3) Is manipulating these AD attributes sufficient?

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image_thumb_6.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image_6.png)

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image_thumb_7.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image_7.png)

Now the reveal:

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image_thumb_8.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image_8.png)

It works!

4) Well I came up with another question – What happens if the AD programmer forgets to manipulate both attributes?

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image_thumb_9.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image_9.png)

If it is missing from Display but is in Search

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image_thumb_10.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image_10.png)

Then it isn’t visible in the Address Book but a search returns it as a result:

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image_thumb_11.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image_11.png)

6) so what if I put MountedProjector back in Display but it is missing from Search?

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image_thumb_12.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image_12.png)

It shows up but a search for MountedProjector reveals nothing:

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image_thumb_13.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image_13.png)

Whereas as search for Whiteboard:

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image_thumb_14.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/81f9f4fbd19b_133C8/image_14.png)

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices