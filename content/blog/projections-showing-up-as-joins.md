---
title: 'Projections showing up as Joins?'
date: 2008-10-08T14:27:00.001-07:00
draft: false
url: /2008/10/projections-showing-up-as-joins.html
tags: 
- ILM
- ILM 2 Beta 3
---

[https://connect.microsoft.com/feedback/ViewFeedback.aspx?FeedbackID=373881&SiteID=433](https://connect.microsoft.com/feedback/ViewFeedback.aspx?FeedbackID=373881&SiteID=433 "https://connect.microsoft.com/feedback/ViewFeedback.aspx?FeedbackID=373881&SiteID=433")

So I found a slight inconsistency when following some of the ILM 2 walk-throughs. When you setup an inbound synch rule that creates objects in ILM the lineage says that the connector space object became a connector through join rules instead of projection rules. Minor bug -- but it sure can be confusing.

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/ProjectionsshowingupasJoins_C61F/image_thumb.png)](http://www.ilmbestpractices.com/blog/uploaded_images/ProjectionsshowingupasJoins_C61F/image.png)

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/ProjectionsshowingupasJoins_C61F/image_thumb_3.png)](http://www.ilmbestpractices.com/blog/uploaded_images/ProjectionsshowingupasJoins_C61F/image_3.png)

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/ProjectionsshowingupasJoins_C61F/image_thumb_4.png)](http://www.ilmbestpractices.com/blog/uploaded_images/ProjectionsshowingupasJoins_C61F/image_4.png)

HR Inbound Sync Rule

General Information

Created Time

8/27/2008 8:10:09 PM

Connected System

{0cd165ec-2745-4afd-95c0-a8f7dbeefe44}

Connected Object Type

person

ILM Object Type

managed:Person

Precedence

1

Create ILM Object

True

Create Connected System Object

False

Disconnect Connected System Object

False

Flow Type

Inbound

Relationships

ILM Attribute

Data Source Attribute

managed:EmployeeID

EmployeeID

Parameters

Parameter Name

Type

Initial Import Flows

Destination

Source

managed:EmployeeID

EmployeeID

Persistent Import Flows

Destination

Source

managed:AccountName

UserID

managed:Company

Company

managed:FirstName

FirstName

managed:LastName

LastName

managed:Manager

Manager

managed:EmployeeType

EmployeeType

managed:DisplayName

FirstName  +  " "  +  LastName

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices