---
title: 'Property Sets for Permissions in AD and AD LDS'
date: 2011-12-26T12:46:00.001-07:00
draft: false
url: /2011/12/property-sets-for-permissions-in-ad-and.html
tags: 
- PowerShell
- AD LDS
- AD
---

A while back I needed to set up Property Sets in AD LDS for granting of permissions to many of the attributes on the person object all at once, as I reviewed the Technet documentation on [AD Property Sets](http://technet.microsoft.com/en-us/library/cc755430(WS.10).aspx) I realized that it doesn’t tell you what object type property sets are, nor does it tell you how to create a property set, nor does it tell you how to assign an attribute to a property set. The [MSDN documentation on Property Sets](http://msdn.microsoft.com/en-us/library/ms683990(v=VS.85).aspx) lets you see which attributes where included in which property sets in the different versions of AD, and it hints that property sets are part of [Control Access Rights](http://msdn.microsoft.com/en-us/library/ms680945(v=VS.85).aspx). Finally there is some more MSDN documentation on [Control Access Rights](http://msdn.microsoft.com/en-us/library/ms675747(v=VS.85).aspx) that starts to spell it out:

> *   For defining property sets, to enable controlling access to a subset of an object's attributes, rather than just to the individual attributes. Using the standard access rights, a single ACE can grant or deny access to all of an object's attributes or to a single attribute. Control access rights provide a way for a single ACE to control access to a set of attributes. For example, the user class supports the **Personal-Information** property set that includes attributes such as street address and telephone number. Property set rights are created on **controlAccessRight** objects by setting the **validAccesses** attribute to contain both the **ACTR\_DS\_READ\_PROP** (16) and the **ACTRL\_DS\_WRITE\_PROP** (32) access rights.

This illustrates the first goal of my post: property sets exist in AD as controlAccessRight objects. But still doesn’t tell us where in the AD do they live. In fact they live in the CN=Extended-Rights container inside the Configuration partition(not the schema):

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/60062c88a23b_ABFA/image_thumb.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/60062c88a23b_ABFA/image.png)

Digging deeper into the MSDN docs on [Creating Control Access Rights](http://msdn.microsoft.com/en-us/library/ms675767(v=VS.85).aspx) illustrates how you link attributes to a property set:

> If you define a control access right for a property set, use the **rightsGUID** of the [**controlAccessRight**](http://msdn.microsoft.com/en-us/library/ms681001(v=VS.85).aspx) object to identify the properties in the set. Every property is defined by an [**attributeSchema**](http://msdn.microsoft.com/en-us/library/ms680969(v=VS.85).aspx) object in the Active Directory schema. The [**attributeSecurityGUID**](http://msdn.microsoft.com/en-us/library/ms675235(v=VS.85).aspx) property of an **attributeSchema** object identifies the property set, if any, that the property belongs to. Be aware that the **attributeSecurityGUID** property is single-valued and stores the GUID in binary format (octet string syntax).

Another goal of this post is to help by making this a little more visual.When you create a property set, you must first generate a GUID and place in the rightsGUID attribute on the controlAccessRights object. To assign an attribute to a property set you need to place this same GUID in the attributeSecurityGUID attribute on the attributeSchema object (in the Schema partition). Remember an attribute can only belong to one property set.

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/60062c88a23b_ABFA/image_thumb_3.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/60062c88a23b_ABFA/image_3.png)

Take a look at the following

[Instructions on how to assign permissions to someone using a Property Set](http://technet.microsoft.com/en-us/library/ff406260.aspx)

For information on how to get the [GUIDs into the right forms see my post](http://blog.ilmbestpractices.com/2011/12/guids-to-octets-guids-to-base64-strings.html)

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices