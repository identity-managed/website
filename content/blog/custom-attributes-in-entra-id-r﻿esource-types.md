---
title: Custom Attributes in Entra ID -- R﻿esource Types
description: "Definitive guide to which way to put custom data into Entra ID:
  Extension Attributes, Directory Extensions, Schema Extensions, or Custom
  Security Attributes. R﻿esource Types"
tags:
  - EntraID;Entra;AzureActiveDirectory;ExtensionAttributes;DirectoryExtensions;SchemaExtensions;CustomSecurityAttributes;
date: 2025-09-26T21:03:55.416Z
banner: /img/all-the-doors-together2.jpg
authors:
  - DavidLundell
---
![](/img/all-the-doors-together2.jpg)

This article is the second in a series about Custom Attributes in Entra ID and will discuss the Resource Types that each of these approaches can use.

1. [Names and aliases](/blog/2025/09/custom-attributes-in-entra-id/#names-and-aliases)
2. [N﻿aming Conventions](/blog/2025/09/custom-attributes-in-entra-id-naming-conventions/)
3. [R﻿esource Types](/blog/2025/09/custom-attributes-in-entra-id-resource-types/)
4. [D﻿ata Types](/blog/2025/09/custom-attributes-in-entra-id-data-types/)
5. [L﻿ifecycle](/blog/2025/09/custom-attributes-in-entra-id-lifecycle/)
6. [L﻿imitations](/blog/2025/09/custom-attributes-in-entra-id-limitations/)
7. [U﻿se Cases](/blog/2025/09/custom-attributes-in-entra-id-use-cases/)
8. [Decision Tree](/blog/2025/09/custom-attributes-in-entra-id-decision-tree/)

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |    
| Resource Types | [Extension attributes](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#extension-attributes) | [Directory Extensions](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#directory-microsoft-entra-id-extensions) | [Schema Extensions](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#schema-extensions) | [Open Extensions](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#open-extensions) | [Custom Security Attributes](https://learn.microsoft.com/en-us/entra/fundamentals/custom-security-attributes-overview) |
| [servicePrincipal](https://learn.microsoft.com/en-us/graph/api/resources/servicePrincipal?view=graph-rest-1.0) | <p style="color:red">NO</p>   | <p style="color:red">NO</p>   | <p style="color:red">NO</p>   | <p style="color:red">NO</p>   | Y   |
| [user](https://learn.microsoft.com/en-us/graph/api/resources/user?view=graph-rest-1.0) | Y   | Y   | Y   | Y   | Y   |
| [device](https://learn.microsoft.com/en-us/graph/api/resources/device?view=graph-rest-1.0) | Y   | Y   | Y   | Y   | <p style="color:red">NO</p>   |
| [group](https://learn.microsoft.com/en-us/graph/api/resources/group?view=graph-rest-1.0) | <p style="color:red">NO</p>   | Y   | Y   | Y   | <p style="color:red">NO</p>   |
| [administrative unit](https://learn.microsoft.com/en-us/graph/api/resources/administrativeunit?view=graph-rest-1.0) | <p style="color:red">NO</p>   | Y   | Y   | <p style="color:red">NO</p>   | <p style="color:red">NO</p>   |
| [application](https://learn.microsoft.com/en-us/graph/api/resources/application?view=graph-rest-1.0) | <p style="color:red">NO</p>   | Y   | <p style="color:red">NO</p>   | <p style="color:red">NO</p>   | <p style="color:red">NO</p>   |
| [organization](https://learn.microsoft.com/en-us/graph/api/resources/organization?view=graph-rest-1.0) | <p style="color:red">NO</p>   | Y   | Y   | Y   | <p style="color:red">NO</p>   |
| [contact](https://learn.microsoft.com/en-us/graph/api/resources/contact?view=graph-rest-1.0) | <p style="color:red">NO</p>   | <p style="color:red">NO</p>   | Y   | Y   | <p style="color:red">NO</p>   |
| [event](https://learn.microsoft.com/en-us/graph/api/resources/event?view=graph-rest-1.0) | <p style="color:red">NO</p>   | <p style="color:red">NO</p>   | Y   | Y   | <p style="color:red">NO</p>   |
| [message](https://learn.microsoft.com/en-us/graph/api/resources/message?view=graph-rest-1.0) | <p style="color:red">NO</p>   | <p style="color:red">NO</p>   | Y   | Y   | <p style="color:red">NO</p>   |
| [post](https://learn.microsoft.com/en-us/graph/api/resources/post?view=graph-rest-1.0) | <p style="color:red">NO</p>   | <p style="color:red">NO</p>   | Y   | Y   | <p style="color:red">NO</p>   |
| [todoTask](https://learn.microsoft.com/en-us/graph/api/resources/todoTask?view=graph-rest-1.0) | <p style="color:red">NO</p>   | <p style="color:red">NO</p>   | <p style="color:red">NO</p>   | Y   | <p style="color:red">NO</p>   |
| [todoTaskList](https://learn.microsoft.com/en-us/graph/api/resources/todoTaskList?view=graph-rest-1.0) | <p style="color:red">NO</p>   | <p style="color:red">NO</p>   | <p style="color:red">NO</p>   | Y   | <p style="color:red">NO</p>   |
|     |     |     |     |     |     |
