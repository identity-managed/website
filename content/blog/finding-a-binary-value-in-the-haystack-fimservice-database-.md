---
title: 'Finding a Binary Value in the Haystack (FIMService Database)'
date: 2010-07-09T14:25:00.001-07:00
draft: false
url: /2010/07/finding-binary-value-in-haystack.html
tags: 
- SQL
- Forefront Identity Manager
- FIM
---

While Query the FIM Service Database at the SQL layer is not supported by Microsoft I had an issue the other day where I couldn’t find what object had a conflicting SID that was preventing the update of another user. I could see in the error detail that it referenced the ObjectSID attribute. So I created this script and replaced the binary value down below with the SID of the object I was looking for.

This SQL Script will find any person object that has any binary attribute with this value in it.

USE FIMSERVICE

GO

SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED

GO

select \* from fim.Objects where \[ObjectKEY\] IN (

select ObjectKey from fim.ObjectValueBinary where ObjectKey in

(

select ObjectKey from fim.Objects o

where o.ObjectTypeKey = (SELECT oti.\[key\] from fim.ObjectTypeInternal oti where Name = 'person')

)

and ValueBinary = 0x010200000000000916000000C83BFC025A1C2A4F9175596438570000

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices