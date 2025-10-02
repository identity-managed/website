---
title: Custom Attributes in Entra ID -- Decision Tree
description: "Definitive guide to which way to put custom data into Entra ID:
  Extension Attributes, Directory Extensions, Schema Extensions, or Custom
  Security Attributes. Decision Tree."
tags:
  - EntraID;Entra;AzureActiveDirectory;ExtensionAttributes;DirectoryExtensions;SchemaExtensions;CustomSecurityAttributes;
date: 2025-10-01T22:41:06.145Z
banner: /img/all-the-doors-together2.jpg
authors:
  - DavidLundell
---
![](/img/all-the-doors-together2.jpg)

This article is the eighth in a series about Custom Attributes in Entra ID and will step through the decision tree which I hope will be the definitive guide to which way to store custom data in Entra ID.

1. [Names and aliases](/blog/2025/09/custom-attributes-in-entra-id/#names-and-aliases)
2. [N﻿aming Conventions](/blog/2025/09/custom-attributes-in-entra-id-naming-conventions/)
3. [R﻿esource Types](/blog/2025/09/custom-attributes-in-entra-id-resource-types/)
4. [D﻿ata Types](/blog/2025/09/custom-attributes-in-entra-id-data-types/)
5. [L﻿ifecycle](/blog/2025/09/custom-attributes-in-entra-id-lifecycle/)
6. [L﻿imitations](/blog/2025/10/custom-attributes-in-entra-id-limitations/)
7. [U﻿se Cases](/blog/2025/10/custom-attributes-in-entra-id-use-cases/)
8. [Decision Tree](/blog/2025/10/custom-attributes-in-entra-id-decision-tree/)

![](/img/entra-id-custom-attribute-decision-tree.png "Entra ID Custom Attribute Decision Tree")

1. **I﻿s this custom data intended for Enterprise Applications or Managed Identities (both of which are of the [servicePrincipal resource type](https://learn.microsoft.com/en-us/graph/api/resources/servicePrincipal?view=graph-rest-1.0))?** 
   *If "Yes," then you must use [Custom Security Attributes](https://learn.microsoft.com/en-us/entra/fundamentals/custom-security-attributes-overview) -- this is the only way to [filter on Applications in Conditional Access Policies](https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-filter-for-applications)*
2. **I﻿s this custom data that you need to [make visible on the Profile Card](https://learn.microsoft.com/en-us/graph/add-properties-profilecard)?** 
   *Then it must be [Extension Attributes](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#extension-attributes)*
3. **W﻿ill this custom data be used in the rules in an [Exchange Online Dynamic Distribution Group](https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/manage-dynamic-distribution-groups/create-manage-dynamic-distribution-groups?source=recommendations&tabs=create-new-eac%2Ccreate-new-eac-2%2Ccreate-new-eac-3)?** 
   *Then it must be [Extension Attributes](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#extension-attributes)*
4. W﻿ill this data be used to [Filter on Devices in Conditional Access Policies](https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-condition-filters-for-devices#supported-operators-and-device-properties-for-filters)? 
   Then it must be [Extension Attributes](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#extension-attributes)
5. D﻿o you need to sync this custom data from On-Premises Active Directory? 
   Then it could be Extension Attributes ﻿but because of the limitations of only having 15 Extension Attributes and the three previous use cases that we can only satisfy with Extension Attributes, you should use Directory Extensions through Entra ID Connect Sync or Entra ID Cloud Sync.
6. Is this custom data to be used in Dynamic membership rules for Distribution Groups or Administrative Units?
   S﻿ame answer as above: it could Extension Attributes but should be Directory Extensions.
7. Do you need to sync this data to another tenant through Cross Tenant Sync?
   S﻿ame answer.
   8﻿. Do you need to provision this data into Entra ID from your HR systems?
   S﻿ame answer.
   9﻿. Do you need to synchronize this data when provisioning to Cloud Apps?
   S﻿ame answer.
   1﻿0. Do you need this data to be available to applications that use Entra ID Domain Services?
   S﻿ame answer.
   1﻿1. Do you need this to be included in SAML and SSO tokens?
   M﻿ostly the same answer. There are ways to include Custom Security Attributes, or data from entirely different sources, such as HR or CRM into the tokens.
   1﻿2. Will this be part of the External ID Custom User Attributes?
   T﻿hen it you must use the UI provided and this will create Directory Extensions on the application.
   1﻿3. Is this sensitive data you need to store on users? And you need to lock down who can read it and who can write it?
   T﻿hen you must Custom Security Attributes.
   1﻿4. Do you need Lifecycle Control over the attribute definitions? I.e. Someone can't delete the definition and render your data undiscoverable.
   Then Schema Extensions or Custom Security Attributes (only if it is to be on users or servicePrincipals).
   1﻿5. Do you need it to be Graph Filterable?
   T﻿hen you can't use Open Extensions
8. I﻿f not Graph Filterable and is it to be on todoTask or todoTaskList? 
   Then you must use Open Extensions
   1﻿7. If not todoTask or todoTaskList is it for the other Outlook resources (contact, Event, Message or Post)?
   T﻿hen you must do Schema Extensions
   1﻿8. Do you need to share this with other tenants without creating a multi-tenant application?
   T﻿hen you must do Schema Extensions
   1﻿9. If you don't need to share it with other tenants and it is on a directory resource
   T﻿hen you can choose between Directory Extensions and Schema Extensions. But I recommend Directory Extensions.

[<- Previous -- U﻿se Cases](/blog/2025/10/custom-attributes-in-entra-id-use-cases/)