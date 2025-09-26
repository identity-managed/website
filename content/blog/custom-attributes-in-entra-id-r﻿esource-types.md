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


<table border=0 cellpadding=0 cellspacing=0 width=641 style='border-collapse:
 collapse;table-layout:fixed;width:482pt'>
 <col width=137 style='mso-width-source:userset;mso-width-alt:4653;width:103pt'>
 <col width=100 style='mso-width-source:userset;mso-width-alt:3373;width:75pt'>
 <col width=108 style='mso-width-source:userset;mso-width-alt:3644;width:81pt'>
 <col width=102 span=2 style='mso-width-source:userset;mso-width-alt:3463;
 width:77pt'>
 <col width=92 style='mso-width-source:userset;mso-width-alt:3117;width:69pt'>
 <tr height=74 style='height:55.35pt'>
  <td height=74 class=xl69 align=left width=137 style='height:55.35pt;
  width:103pt'>Resource Types</td>
  <td class=xl73 align=left width=100 style='width:75pt'><a
  href="https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#extension-attributes"
  target="_parent"><span style='font-size:14.0pt;font-weight:700'>Extension
  attributes</span></a></td>
  <td class=xl76 align=left width=108 style='border-left:none;width:81pt'><a
  href="https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#directory-microsoft-entra-id-extensions"
  target="_parent"><span style='font-size:14.0pt;font-weight:700'>Directory
  Extensions</span></a></td>
  <td class=xl75 align=left width=102 style='border-left:none;width:77pt'><a
  href="https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#schema-extensions"
  target="_parent"><span style='font-size:14.0pt;font-weight:700'>Schema
  Extensions</span></a></td>
  <td class=xl75 align=left width=102 style='border-left:none;width:77pt'><a
  href="https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#open-extensions"
  target="_parent"><span style='font-size:14.0pt;font-weight:700'>Open
  Extensions</span></a></td>
  <td class=xl75 align=left width=92 style='border-left:none;width:69pt'><a
  href="https://learn.microsoft.com/en-us/entra/fundamentals/custom-security-attributes-overview"
  target="_parent"><span style='font-size:14.0pt;font-weight:700'>Custom
  Security Attributes</span></a></td>
 </tr>
 <tr height=19 style='height:14.35pt'>
  <td height=19 class=xl72 align=left style='height:14.35pt'><a
  href="https://learn.microsoft.com/en-us/graph/api/resources/servicePrincipal?view=graph-rest-1.0"
  target="_parent">servicePrincipal</a></td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
 </tr>
 <tr height=19 style='height:14.35pt'>
  <td height=19 class=xl72 align=left style='height:14.35pt'><a
  href="https://learn.microsoft.com/en-us/graph/api/resources/user?view=graph-rest-1.0"
  target="_parent">user</a></td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
 </tr>
 <tr height=19 style='height:14.35pt'>
  <td height=19 class=xl72 align=left style='height:14.35pt'><a
  href="https://learn.microsoft.com/en-us/graph/api/resources/device?view=graph-rest-1.0"
  target="_parent">device</a></td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
 </tr>
 <tr height=19 style='height:14.35pt'>
  <td height=19 class=xl72 align=left style='height:14.35pt'><a
  href="https://learn.microsoft.com/en-us/graph/api/resources/group?view=graph-rest-1.0"
  target="_parent">group</a></td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
 </tr>
 <tr height=19 style='height:14.35pt'>
  <td height=19 class=xl72 align=left style='height:14.35pt'><a
  href="https://learn.microsoft.com/en-us/graph/api/resources/administrativeunit?view=graph-rest-1.0"
  target="_parent">administrative unit</a></td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
 </tr>
 <tr height=19 style='height:14.35pt'>
  <td height=19 class=xl72 align=left style='height:14.35pt'><a
  href="https://learn.microsoft.com/en-us/graph/api/resources/application?view=graph-rest-1.0"
  target="_parent">application</a></td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
 </tr>
 <tr height=19 style='height:14.35pt'>
  <td height=19 class=xl72 align=left style='height:14.35pt'><a
  href="https://learn.microsoft.com/en-us/graph/api/resources/organization?view=graph-rest-1.0"
  target="_parent">organization</a></td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
 </tr>
 <tr height=19 style='height:14.35pt'>
  <td height=19 class=xl72 align=left style='height:14.35pt'><a
  href="https://learn.microsoft.com/en-us/graph/api/resources/contact?view=graph-rest-1.0"
  target="_parent">contact</a></td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
 </tr>
 <tr height=19 style='height:14.35pt'>
  <td height=19 class=xl72 align=left style='height:14.35pt'><a
  href="https://learn.microsoft.com/en-us/graph/api/resources/event?view=graph-rest-1.0"
  target="_parent">event</a></td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
 </tr>
 <tr height=19 style='height:14.35pt'>
  <td height=19 class=xl72 align=left style='height:14.35pt'><a
  href="https://learn.microsoft.com/en-us/graph/api/resources/message?view=graph-rest-1.0"
  target="_parent">message</a></td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
 </tr>
 <tr height=19 style='height:14.35pt'>
  <td height=19 class=xl72 align=left style='height:14.35pt'><a
  href="https://learn.microsoft.com/en-us/graph/api/resources/post?view=graph-rest-1.0"
  target="_parent">post</a></td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
 </tr>
 <tr height=19 style='height:14.35pt'>
  <td height=19 class=xl72 align=left style='height:14.35pt'><a
  href="https://learn.microsoft.com/en-us/graph/api/resources/todoTask?view=graph-rest-1.0"
  target="_parent">todoTask</a></td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
 </tr>
 <tr height=19 style='height:14.35pt'>
  <td height=19 class=xl72 align=left style='height:14.35pt'><a
  href="https://learn.microsoft.com/en-us/graph/api/resources/todoTaskList?view=graph-rest-1.0"
  target="_parent">todoTaskList</a></td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
  <td class=xl67 style='font-size:11.0pt;color:#006100;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#C6EFCE;mso-pattern:black none'>Y</td>
  <td class=xl67 style='font-size:11.0pt;color:#9C0006;font-weight:400;
  text-decoration:none;text-underline-style:none;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;background:#FFC7CE;mso-pattern:black none'>N</td>
 </tr>
 <![if supportMisalignedColumns]>
 <tr height=0 style='display:none'>
  <td width=137 style='width:103pt'></td>
  <td width=100 style='width:75pt'></td>
  <td width=108 style='width:81pt'></td>
  <td width=102 style='width:77pt'></td>
  <td width=102 style='width:77pt'></td>
  <td width=92 style='width:69pt'></td>
 </tr>
 <![endif]>
</table>


