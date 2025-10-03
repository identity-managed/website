---
title: Custom Attributes in Entra ID -- N﻿aming Conventions
description: "Definitive guide to which way to put custom data into Entra ID:
  Extension Attributes, Directory Extensions, Schema Extensions, or Custom
  Security Attributes. Naming conventions"
tags:
  - EntraID;Entra;AzureActiveDirectory;ExtensionAttributes;DirectoryExtensions;SchemaExtensions;CustomSecurityAttributes;
date: 2025-09-26T20:20:33.887Z
banner: /img/all-the-doors-together2.jpg
authors:
  - DavidLundell
---
![](/img/all-the-doors-together2.jpg)

This article is the second in a series about Custom Attributes in Entra ID and will discuss the N﻿aming Conventions so that you can recognize them when you see them in the wild and understand how uniqueness is enforced and guaranteed.

1. [Names and aliases](/blog/2025/09/custom-attributes-in-entra-id/#names-and-aliases)
2. [N﻿aming Conventions](/blog/2025/09/custom-attributes-in-entra-id-naming-conventions/)
3. [R﻿esource Types](/blog/2025/09/custom-attributes-in-entra-id-resource-types/)
4. [D﻿ata Types](/blog/2025/09/custom-attributes-in-entra-id-data-types/)
5. [L﻿ifecycle](/blog/2025/09/custom-attributes-in-entra-id-lifecycle/)
6. [L﻿imitations](/blog/2025/10/custom-attributes-in-entra-id-limitations/)
7. [U﻿se Cases](/blog/2025/10/custom-attributes-in-entra-id-use-cases/)
8. [Decision Tree](/blog/2025/10/custom-attributes-in-entra-id-decision-tree/)

|                                                                                                                                          |                                                                                                                                                                                                        |                                                                 |                                                                                                                                                                                                                                                                                                                                                                |
| ---------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Names                                                                                                                                    | Name or ID                                                                                                                                                                                             | Example                                                         | Notes                                                                                                                                                                                                                                                                                                                                                          |
| [Extension attributes](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#extension-attributes)                    | [extensionAttribute1 .. extensionAttribute15](https://learn.microsoft.com/en-us/graph/api/resources/onpremisesextensionattributes?view=graph-rest-1.0)                                                 | extensionAttribute15                                            | The names are already pre-determined                                                                                                                                                                                                                                                                                                                           |
| [Directory Extensions](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#directory-microsoft-entra-id-extensions) | extension_ {ApplicationId}_attributeName                                                                                                                                                               | extension_ 4b2af6e7f3ac4f598e35c364e0126c6d _MgrLvl             | The Application ID or Client ID (not the object ID of the Application)                                                                                                                                                                                                                                                                                         |
| [Schema Extensions](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#schema-extensions)                          | [verifiedVanityDomain*extensionID  <br>OR  <br>ext{﻿8-random-alphanumeric-chars}*{﻿schema-name}](https://learn.microsoft.com/en-us/graph/api/resources/schemaextension?view=graph-rest-1.0#properties) | snappyslackers_coordinates  <br>OR  <br>extwmo14pts_coordinates | [You can choose between using the verified Vanity Domain Name or allowing EntraID to generate a random prefix for you](https://learn.microsoft.com/en-us/graph/extensibility-schema-groups?tabs=http#step-2-register-a-schema-extension-definition)                                                                                                            |
| [Open Extensions](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#open-extensions)                              | [ReverseFQDN.extensionName](https://learn.microsoft.com/en-us/graph/api/resources/opentypeextension?view=graph-rest-1.0)                                                                               | com.snappyslackers.coordinates                                  | It looks like this is an unenforced convention                                                                                                                                                                                                                                                                                                                 |
| [Custom Security Attributes](https://learn.microsoft.com/en-us/entra/fundamentals/custom-security-attributes-overview)                   | [<AttributeSetName_AttributeName>](https://learn.microsoft.com/en-us/graph/api/resources/customsecurityattributedefinition?view=graph-rest-1.0#properties)                                             | HR_MgrLvl                                                       | [Both the AttributeSetName and the AttributeName can be up to 32 Unicode Characters with neither spaces nor specials characters.  <br>AttributeName must be unique within its Attribute set, which in turn must be unique within the tenant.](https://learn.microsoft.com/en-us/entra/fundamentals/custom-security-attributes-overview#limits-and-constraints) |
|                                                                                                                                          |                                                                                                                                                                                                        |                                                                 |                                                                                                                                                                                                                                                                                                                                                                |

## Extension Attributes

Y﻿ou do not get to choose the names of the Extension Attributes as they are predetermined and fixed. 

## On-premises Active Directory

W﻿ith on-premises Active Directory and any LDAP directory you could have collisions with attribute names but at least the [Object Identifier (OID)](https://learn.microsoft.com/en-us/windows/win32/ad/obtaining-an-object-identifier) enforced uniqueness, right? Sort of. You could use the OID registrar and get a unique OID or generate one through Microsoft using your script to generate an OID with a random GUID. But nothing prevented you from making your own AD schema extension and using someone else's OID or prevent them from using yours, except common sense, which always prevails!

## Directory Extension names are yucky!

When you create a Directory Extension you get stuck with using the Application ID (a GUID) as part of the name . Yuck! But this **guarantees uniqueness throughout the known universe**, and when building a multi-tenant app or installing a multi-tenant app that someone else built this is critical! (note this is not the ObjectID of the Registered Application nor the ObjectID of the related Enterprise Application, but the AppID or Client ID of the application -- *this number shows up on both the Registered Application and all of its related Enterprise Applications*).

## Schema Extensions are prettier!

T﻿o enforce uniqueness you can use a vanity domain or let Entra generate a prefix of "ext" followed by 8 random characters and then it adds the name you provide. The **vanity domain is highly recommended** for two reasons:

![](/img/schema-extensions-small.jpg)

\
1﻿. You can pick it and make all of your schema extensions consistent
2﻿. While the Schema Extension is in the InDevelopment status should you delete the extension before nulling out or deleting the data on the resources you can recreate the Schema Extension and then null out the data. This is not possible if you let Entra generate the random prefix. 

## O﻿pen Extensions are the wild wild west and you can name it whatever you want

![](/img/open-extension-batwing-doors-small.png)

## C﻿ustom Security Attributes

C﻿ustom Security Attributes names start with the name of the AttributeSet and then an underscore and then the name of the attribute. In terms of naming conventions I like this the best. Since these are limited to your tenant they only need to be unique inside your tenant.

![](/img/custom-security-attributes-vault-door-small.png)

[<- Previous -- Names and aliases](/blog/2025/09/custom-attributes-in-entra-id/#names-and-aliases)\
[Next -- R﻿esource Types ->](/blog/2025/09/custom-attributes-in-entra-id-resource-types/)