---
title: 'FIM RCDC explained in brief'
date: 2009-11-29T09:50:00.001-07:00
draft: false
url: /2009/11/fim-rcdc-explained-in-brief.html
tags: 
- Forefront Identity Manager
- ILM
- Identity Management
- FIM
---

In this post I attempt to give you the reader a quick overview of how the FIM RCDC works conceptually. As for the mechanics of modifying the RCDC the nearly complete but growing collection of documents downloadable from MSFT will suffice.

As you will recall FIM is the new abbreviation for ILM, since it has been renamed Forefront Identity Manager, and RCDC is the Resource Control Display Configuration formerly known as the Object Visualization Configuration (OVC). RCDC is the way you custom how FIM displays objects (now called resources) in the portal. Now for English: If you need to change the options and information users see in the FIM portal when they create new users, groups (security or distribution), or edit or view these resources you do it by modifying the RCDC. The RCDC is an XML object, and each resource type (user, group, request, etc) has three: Create, Edit and View. To get a handle on the terms take a look at the figure below:

[![RCDCExplained](http://www.ilmbestpractices.com/blog/uploaded_images/FIMRCDCexplainedinbrief_8A30/RCDCExplained_thumb.jpg "RCDCExplained")](http://www.ilmbestpractices.com/blog/uploaded_images/FIMRCDCexplainedinbrief_8A30/RCDCExplained.jpg)

Every RCDC has a Panel that contains all other visible elements. You don’t have to worry about the Panel, other than to know that you need a have it and it must have a name.

The next item to which I must call your attention is the Groupings. The little area which I have outlined in Red is the Header Grouping and provides the caption for the RCDC in this case: Create Security Group. The Header Grouping contains just one control the UocCaptionControl and it is this control that determines what will be displayed based on the Caption and Description Attributes.

The rest of the groupings show up as tabs. The first three are content groupings (there can be up. to 16 groupings counting the Header Grouping and the Summary Grouping, leave up to 14 slots for content groupings). Each content tab or grouping can contain between 1 and 256 controls.

Not visible in the screenshot above are data sources. Data sources provide access to the data of the resource (PrimaryResourceObjectDataSource), the changes that are being made during the edit or create process (PrimaryResourceDeltaDataSource), what rights the current user has to each attribute (PrimaryResourceRightsDataSource), information about the resource type and its attribute types, such as displayname and description (SchemaDataSource), and a listing of Active Directory Domains that are managed by this instance of FIM (DomainDataSource). Additionally, you can have XML data sources. There are two purposes for these: 1) to provide the xsl transformation to provide a different summary of changes on the Grouping Summary, and 2) to provide a list for use in UocDropDownList and UocRadioButtonList controls (there is at least one other method for providing the options list).

Controls have elements, and attributes. The element type you will be concerned with are the Properties. (Help only applies to groupings, CustomProperties is not supported, Options only applies to the UocDropDownList and UocRadioButtonList controls, Buttons only applies to the UoCListView Control, and you can’t make use of events.)

The attributes and properties are used to govern the behavior of the control. They can be bound to the different data sources, to cause the control to interact with an attribute on a resource, to control the visibility and editing on a control, and to provide the list of options to choose from.

Well that covers the conceptual overview. Next time I blog about RCDC, I plan on discussing the attributes of controls, and their common properties.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices