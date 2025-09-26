---
title: Custom Attributes in Entra ID
description: "Definitive guide to which way to put custom data into Entra ID:
  Extension Attributes, Directory Extensions, Schema Extensions, or Custom
  Security Attributes"
tags:
  - EntraID;Entra;AzureActiveDirectory;ExtensionAttributes;DirectoryExtensions;SchemaExtensions;CustomSecurityAttributes;
date: 2025-09-26T06:41:28.455Z
banner: /img/all-the-doors-together2.png
authors:
  - DavidLundell
---
M﻿icrosoft has had a lot of chefs in the kitchen baking up solutions to different problems and now we have an array of confusing choices about where to put your data. This is the first of a series of posts to help you choose the correct one for you and your needs.

![](/img/all-the-doors-together2.png)

I﻿n some ways the easiest to use (Extension Attributes) can also be the hardest since you have to manage the population of the data very differently depending on whether the user is synced from on-premises AD or is cloud only. This limited resource is also the most important to choose what to do with since there are some use cases such as viewing on the profile card that only work for Extension Attributes.

W﻿e will start with their: 

1. Names and aliases 

   1. so that you can realize when documentation and posts are talking about them
2. N﻿aming Conventions

   1. So that you can recognize them when you see them in the wild 
3. R﻿esource Types
4. D﻿ata Types
5. L﻿ifecycle
6. L﻿imitations
7. U﻿se Cases

T﻿hen we will present a decision tree to help you decide.

# Names and aliases

|                                                                                                                                          |                                                                                                                                          |                                                                                                                         |
| ---------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| Names                                                                                                                                    | Alias                                                                                                                                    | Additional Alias                                                                                                        |
| [Extension attributes](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#extension-attributes)                    | [onPremisesExtensionAttributes](https://learn.microsoft.com/en-us/graph/api/resources/onpremisesextensionattributes?view=graph-rest-1.0) | [Custom attributes in Exchange Server](https://learn.microsoft.com/en-us/exchange/recipients/mailbox-custom-attributes) |
| [Directory Extensions](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#directory-microsoft-entra-id-extensions) | Custom Extension Attributes in Azure AD/Entra ID                                                                                         | Azure AD/Entra ID Connect Sync Directory Extensions                                                                     |
| [Schema Extensions](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#schema-extensions)                          | [Microsoft Graph schema extensions](https://learn.microsoft.com/en-us/graph/api/resources/schemaextension)                               |                                                                                                                         |
| [Open Extensions](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#open-extensions)                              | [openTypeExtension](https://learn.microsoft.com/en-us/graph/api/resources/opentypeextension?view=graph-rest-1.0)                         |                                                                                                                         |
| [Custom Security Attributes](https://learn.microsoft.com/en-us/entra/fundamentals/custom-security-attributes-overview)                   |                                                                                                                                          |                                                                                                                         |
|                                                                                                                                          |                                                                                                                                          |                                                                                                                         |