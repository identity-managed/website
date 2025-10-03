---
title: Custom Attributes in Entra ID
description: "Definitive guide to which way to put custom data into Entra ID:
  Extension Attributes, Directory Extensions, Schema Extensions, or Custom
  Security Attributes"
tags:
  - EntraID;Entra;AzureActiveDirectory;ExtensionAttributes;DirectoryExtensions;SchemaExtensions;CustomSecurityAttributes;
date: 2025-09-26T06:41:28.455Z
banner: /img/all-the-doors-together2.jpg
authors:
  - DavidLundell
---
Microsoft has had a lot of chefs in the Entra ID kitchen baking up solutions to different problems and now we have an array of confusing choices about where to put your data.  

![](/img/all-the-doors-together2.jpg "The 5 doors of Entra ID Custom Data")

This is the first of a series of posts to help you choose the correct one for you and your needs. 

While Microsoft's official documentation provides a [fairly handy comparison table](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#comparison-of-extension-types) it **completely leaves out Custom Security Attributes**. Overall, I find that there are some gaps, and a couple of contradictions but not a definitive guide to help you know when to use which extension.

In on-premises Active Directory(AD) we only had two choices :

* [Extension Attributes](https://learn.microsoft.com/en-us/exchange/recipients/mailbox-custom-attributes)  [](https://learn.microsoft.com/en-us/windows/win32/ad/how-to-extend-the-schema)
* [Schema Extensions](https://learn.microsoft.com/en-us/windows/win32/ad/how-to-extend-the-schema)
  Additionally, we could create new object classes not just attributes.

The Extension Attributes were not part of the AD Schema until you applied the Exchange Schema Extensions a﻿nd were created to give you 15 pre-canned places to put some custom string data without having to go through the scary and irreversible process of 

> EXTENDING THE SACRED ACTIVE DIRECTORY SCHEMA! 

But you also couldn't clearly label the attributes nor could you constrain by data type or anything else. The [Extension Attributes in Entra](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#extension-attributes) are the cloud version of these. 

In contrast AD Schema Extensions don't have a perfect parallel in the Entra. Whereas [Directory Extensions](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#directory-microsoft-entra-id-extensions), [Schema Extensions](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#schema-extensions) and [Custom Security Attributes](https://learn.microsoft.com/en-us/entra/fundamentals/custom-security-attributes-overview) all have similarities to the on-premises AD Schema Extensions, [Open Extensions](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#open-extensions) are a completely different animal evoking images of the Wild West, where anything goes! 

I﻿n some ways the easiest to use (Extension Attributes) can also be the hardest since you have to manage the population of the data very differently depending on whether the user is synced from on-premises AD or is cloud only. This limited resource is also the most important to choose what to do with since there are some use cases such as viewing on the profile card that only work for Extension Attributes.

W﻿e will start with their: 

1. [Names and aliases](/blog/2025/09/custom-attributes-in-entra-id/#names-and-aliases)

   1. so that you can realize when documentation and posts are talking about them
2. [N﻿aming Conventions](/blog/2025/09/custom-attributes-in-entra-id-naming-conventions/)

   1. So that you can recognize them when you see them in the wild 
3. [R﻿esource Types](/blog/2025/09/custom-attributes-in-entra-id-resource-types/)
4. [D﻿ata Types](/blog/2025/09/custom-attributes-in-entra-id-data-types/)
5. [L﻿ifecycle](/blog/2025/09/custom-attributes-in-entra-id-lifecycle/)
6. [L﻿imitations](/blog/2025/10/custom-attributes-in-entra-id-limitations/)
7. [U﻿se Cases](/blog/2025/10/custom-attributes-in-entra-id-use-cases/)
8. [Decision Tree](/blog/2025/10/custom-attributes-in-entra-id-decision-tree/)

T﻿he decision tree to help you decide what works best for you.

# Names and aliases ("an \[extension] by any other name would" make web searches more confusing)

|                                                                                                                                          |                                                                                                                                          |                                                                                                                                                                                                                          |
| ---------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Names**                                                                                                                                | **Alias**                                                                                                                                | **Additional Alias**                                                                                                                                                                                                     |
| [Extension attributes](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#extension-attributes)                    | [onPremisesExtensionAttributes](https://learn.microsoft.com/en-us/graph/api/resources/onpremisesextensionattributes?view=graph-rest-1.0) | [Custom attributes in Exchange Server](https://learn.microsoft.com/en-us/exchange/recipients/mailbox-custom-attributes)                                                                                                  |
| [Directory Extensions](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#directory-microsoft-entra-id-extensions) | Custom Extension Attributes in Azure AD/Entra ID                                                                                         | Azure AD/Entra ID Connect Sync Directory Extensions                                                                                                                                                                      |
| [Schema Extensions](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#schema-extensions)                          | [Microsoft Graph schema extensions](https://learn.microsoft.com/en-us/graph/api/resources/schemaextension)                               |                                                                                                                                                                                                                          |
| [Open Extensions](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#open-extensions)                              | [openTypeExtension](https://learn.microsoft.com/en-us/graph/api/resources/opentypeextension?view=graph-rest-1.0)                         | [O﻿ffice 365 data extensions](https://learn.microsoft.com/en-us/graph/api/resources/extended-properties-overview?view=graph-rest-1.0#use-extended-properties-or-open-extensions:~:text=Office%20365%20data%20extensions) |
| [Custom Security Attributes](https://learn.microsoft.com/en-us/entra/fundamentals/custom-security-attributes-overview)                   |                                                                                                                                          |                                                                                                                                                                                                                          |
|                                                                                                                                          |                                                                                                                                          |                                                                                                                                                                                                                          |

## S﻿chema Extensions

is the most confusing because of the ["Tenant Schema Extension App"](https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-sync-feature-directory-extensions#configuration-changes-in-microsoft-entra-id-made-by-the-wizard) which is registered during the installation of Entra Connect to hold is Directory Extensions. This will frequently turn up when searching the web for "Schema Extensions".

![](/img/schema-extensions-small.jpg)

## D﻿irectory Extensions

are also confusing because they were created to solve the problem for DirSync, of what to do with on premises AD Attributes that don't exist in Entra ID. DirSync which became Azure Active Directory Connect Sync and later Entra Connect Sync. So most of you have heard of these as AAD or Entra Connect Sync Directory Extensions, but they are also called [Custom Extension Attributes in several articles](https://learn.microsoft.com/en-us/entra/identity/hybrid/cloud-sync/how-to-preserve-original-organizational-unit#prerequisite), but so are the [Extension Attributes](https://learn.microsoft.com/en-us/graph/add-properties-profilecard#add-a-custom-attribute-to-the-profile-card). O﻿ne article on [Define custom attributes in Azure Active Directory B2C](https://learn.microsoft.com/en-us/azure/active-directory-b2c/user-flow-custom-attributes?pivots=b2c-custom-policy) on refers to Directory extensions as: 

* e﻿xtension property
* c﻿ustom attribute
* c﻿ustom claim

## O﻿ne more element of confusion:

in the world of Office 365/Outlook resources (completely excluding directory resources) there is a legacy method of storing custom data known as [extended properties](https://learn.microsoft.com/en-us/graph/api/resources/extended-properties-overview?view=graph-rest-1.0). Don't let this be confused with Extension Attributes, Directory Extensions, Schema Extensions, not Open Extensions. This is purely for Outlook resources on users, and groups. Further, the articles recommends using Open Extensions instead of extended properties.

Q﻿uick shoutout to [Merill Fernando](https://merill.net/) for his post in 2023 about the [different ways to extend the Entra ID Schema.](https://merill.net/2023/02/azure-ad-extensions-and-attributes/)

I﻿ am intending to build on and update his good work, which did add Custom Security Attributes to the comparison table and also some use cases.

[\-> Next - N﻿aming Conventions](/blog/2025/09/custom-attributes-in-entra-id-naming-conventions/)