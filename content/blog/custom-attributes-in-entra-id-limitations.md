---
title: Custom Attributes in Entra ID -- Limitations
description: "Definitive guide to which way to put custom data into Entra ID:
  Extension Attributes, Directory Extensions, Schema Extensions, or Custom
  Security Attributes. Limits or Limitations."
tags:
  - EntraID;Entra;AzureActiveDirectory;ExtensionAttributes;DirectoryExtensions;SchemaExtensions;CustomSecurityAttributes;
date: 2025-10-01T02:27:11.630Z
banner: /img/all-the-doors-together2.jpg
authors:
  - DavidLundell
---
![](/img/all-the-doors-together2.jpg)

This article is the sixth in a series about Custom Attributes in Entra ID and will discuss the Limitations of each these approaches.

1. [Names and aliases](/blog/2025/09/custom-attributes-in-entra-id/#names-and-aliases)
2. [N﻿aming Conventions](/blog/2025/09/custom-attributes-in-entra-id-naming-conventions/)
3. [R﻿esource Types](/blog/2025/09/custom-attributes-in-entra-id-resource-types/)
4. [D﻿ata Types](/blog/2025/09/custom-attributes-in-entra-id-data-types/)
5. [L﻿ifecycle](/blog/2025/09/custom-attributes-in-entra-id-lifecycle/)
6. [L﻿imitations](/blog/2025/10/custom-attributes-in-entra-id-limitations/)
7. [U﻿se Cases](/blog/2025/10/custom-attributes-in-entra-id-use-cases/)
8. [Decision Tree](/blog/2025/10/custom-attributes-in-entra-id-decision-tree/)

|                                     |                                                                                                                       |                                                                                                                                          |                                                                                                                                                |                                                                                                             |                                                                                                                        |
| ----------------------------------- | --------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| Limitation                          | [Extension attributes](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#extension-attributes) | [Directory Extensions](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#directory-microsoft-entra-id-extensions) | [Schema Extensions](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#schema-extensions)                                | [Open Extensions](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#open-extensions) | [Custom Security Attributes](https://learn.microsoft.com/en-us/entra/fundamentals/custom-security-attributes-overview) |
| Needs an App to own it              | N                                                                                                                     | Y                                                                                                                                        | Y                                                                                                                                              | N but an App must create it                                                                                 | N                                                                                                                      |
| Values Per Resource                 | 15                                                                                                                    | 100                                                                                                                                      | 100                                                                                                                                            | 2 kb of data                                                                                                | 50                                                                                                                     |
| Per App                             | N/A                                                                                                                   |                                                                                                                                          | 5 definitions                                                                                                                                  | 2 extensions                                                                                                | N/A                                                                                                                    |
| Per Tenant                          | 15                                                                                                                    | Infinte                                                                                                                                  | Infinte                                                                                                                                        | Infinte                                                                                                     | 500                                                                                                                    |
| Schema can be shared                | Built in to every tenant                                                                                              | If other tenants install your mult-tenant app                                                                                            | [Discoverable Globally](https://learn.microsoft.com/en-us/graph/extensibility-schema-groups?tabs=http#step-1-view-available-schema-extensions) | N                                                                                                           | N                                                                                                                      |
| Can exist on Synced User            | Y                                                                                                                     | Y                                                                                                                                        | Y                                                                                                                                              | Y                                                                                                           | Y                                                                                                                      |
| Must Manage on Prem for Synced User | Y                                                                                                                     | N*                                                                                                                                       | N                                                                                                                                              | N                                                                                                           | N                                                                                                                      |
|                                     |                                                                                                                       |                                                                                                                                          |                                                                                                                                                |                                                                                                             |                                                                                                                        |

\*﻿No, except for Directory extensions from the "Tenant Schema Extension App" used by Entra ID Connect Sync and Cloud Sync.

## E﻿xtension Attributes

T﻿he most distinguishing limit is how many extensions/custom attributes each method can have. The Extension Attributes can only have **15** **string attributes per resource** and only on users and devices. While these Extension Attributes have a lot of use cases in the next post we will see that there are some use cases that only Extension Attributes can do. The use cases that can only use Extension Attributes combined with only 15 attributes makes these handy attributes a very valuable resource and not be littered with inconsistent garbage as we often see in on-prem AD.

## C﻿ustom Security Attributes

C﻿ustom Security Attributes can only have **500** attribute definitions whereas the other three (Open, Directory and Schema) can have infinite definitions. On the plus side deactivated definitions do not count against the limit. Further, Custom Security Attributes can only have **50 attribute values populated per resource** (this means a resource having 50 single-valued attributes populated, one particular multi-valued custom security attribute having 50 values or some combination thereof). This limitation and its unique use case can also make this a method to use wisely.

## D﻿irectory Extensions and Schema Extensions

D﻿irectory Extensions and Schema Extensions are both limited to **100 values populated per resource**. Although for Schema Extensions it must be noted that this limitation only applies to directory resources (user, group, adminsitrativeUnit, and organization).

## Open Extensions

Open Extensions can only have two extensions per creator app. Open Extensions have a data size limit per resource rather than a limit in the number of attributes but this also differs depending on the resource type. On directory resources (user, group, device and organization) the **limit is 2 Kb of data.** 

MAPI Named Properties 

Open Extensions on Outlook resources are stored in a [MAPI Named Property](https://learn.microsoft.com/en-us/office/client-developer/outlook/mapi/mapi-named-properties). This imposes different restrictions  on Outlook resources in a user's mailbox (message, event, and contact) than for Open Extensions on directory objects. [The documentation just says that these "are a limited resources in a user's mailbox."](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#comparison-of-extension-types). 

The linked documents on MAPI Named Properties don't explain this, at least not to my satisfaction. But I find discussion about [property identifiers ranges](https://learn.microsoft.com/en-us/office/client-developer/outlook/mapi/property-identifier-ranges). The range for Named Properties goes from 0x8000 to 0xFFFE, allowing for 32,767 Named Properties. I also found a reference to [increasing MAPI property limits in on-prem Exchange Server](https://help.bittitan.com/hc/en-us/articles/1260800182350-Exchange-Mailbox-Migration-Troubleshooting#h_01HS95EZTJW0MN0EHDQKYNK266) which seems to have had a default limit of 8192, which could be changed in the registry. I think this is what they are referring to.

W﻿hile the documentation cited above is not really clear if post, todoTask, and todoTaskList are Outlook resource types, I think they are and therefore those same limits likely apply.

O﻿ne other note about a limitation on Open Extensions [copied from the documentation](https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#comparison-of-extension-types:~:text=Due%20to%20an%20existing%20service%20limitation%2C%20delegates%20can%27t%20create%20open%20extension%2Dappended%20events%20in%20shared%20mailbox%20calendars.%20Attempts%20to%20do%20so%20result%20in%20an%20ErrorAccessDenied%20response.):

> Due to an existing service limitation, delegates can't create open extension-appended events in shared mailbox calendars. Attempts to do so result in an ErrorAccessDenied response.

## S﻿ynced from on-prem

O﻿ne final important distinction has to do with users that are synced from on-prem AD. For users synced from on-prem AD you must manage the Extension Attributes in the on-prem AD, the same is true for a limited set of Directory Extensions -- the ones from the "Tenant Schema Extension App" used by Entra ID Connect Sync and Cloud Sync.

[<- Previous -- L﻿ifecycle](/blog/2025/09/custom-attributes-in-entra-id-lifecycle/)\
[Next -- U﻿se Cases ->](/blog/2025/10/custom-attributes-in-entra-id-use-cases/)