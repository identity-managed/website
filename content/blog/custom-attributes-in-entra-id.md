---
title: Custom Attributes in Entra ID
description: "Definitive guide to which way to put custom data into Entra ID:
  Extension Attributes, Directory Extensions, Schema Extensions, or Custom
  Security Attributes"
tags:
  - EntraID;Entra;AzureActiveDirectory;ExtensionAttributes;DirectoryExtensions;SchemaExtensions;CustomSecurityAttributes;
date: 2025-09-26T06:41:28.455Z
banner: /img/all-the-doors-together.png
authors:
  - DavidLundell
---
M﻿icrosoft has had a lot of chefs in the kitchen baking up solutions to different problems and now we have an array of confusing choices about where to put your data. This is the first of a series of posts to help you choose the correct one for you and your needs.

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


<table border=0 cellpadding=0 cellspacing=0 width=757 style='border-collapse:
 collapse;table-layout:fixed;width:568pt'>
 <col width=283 style='mso-width-source:userset;mso-width-alt:9592;width:212pt'>
 <col width=237 span=2 style='mso-width-source:userset;mso-width-alt:8041;
 width:178pt'>
 <tr height=20 style='height:14.7pt'>
  <td height=20 align=left width=283 style='height:14.7pt;width:212pt;
  font-size:11.0pt;color:white;font-weight:700;text-decoration:none;text-underline-style:
  none;text-line-through:none;font-family:"Aptos Narrow", sans-serif;
  border-top:.5pt solid black;border-right:none;border-bottom:none;border-left:
  .5pt solid black;background:black;mso-pattern:black none'>Names</td>
  <td align=left width=237 style='width:178pt;font-size:11.0pt;color:white;
  font-weight:700;text-decoration:none;text-underline-style:none;text-line-through:
  none;font-family:"Aptos Narrow", sans-serif;border-top:.5pt solid black;
  border-right:none;border-bottom:none;border-left:none;background:black;
  mso-pattern:black none'>Alias</td>
  <td align=left width=237 style='width:178pt;font-size:11.0pt;color:white;
  font-weight:700;text-decoration:none;text-underline-style:none;text-line-through:
  none;font-family:"Aptos Narrow", sans-serif;border-top:.5pt solid black;
  border-right:.5pt solid black;border-bottom:none;border-left:none;background:
  black;mso-pattern:black none'>Additional Alias</td>
 </tr>
 <tr height=24 style='height:18.35pt'>
  <td height=24 class=xl73 align=left width=283 style='height:18.35pt;
  width:212pt;font-size:14.0pt;color:#467886;font-weight:700;text-decoration:
  underline;text-underline-style:single;text-line-through:none;font-family:
  "Aptos Narrow", sans-serif;border-top:1.0pt solid #A3A3A3;border-right:1.0pt solid #A3A3A3;
  border-bottom:none;border-left:1.0pt solid #A3A3A3'><a
  href="https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#extension-attributes"
  target="_parent"><span style='font-size:14.0pt;font-weight:700'>Extension
  attributes</span></a></td>
  <td class=xl71 width=237 style='width:178pt;font-size:11.0pt;color:#467886;
  font-weight:400;text-decoration:underline;text-underline-style:single;
  text-line-through:none;font-family:"Aptos Narrow", sans-serif;border-top:
  .5pt solid black;border-right:none;border-bottom:none;border-left:none'><a
  href="https://learn.microsoft.com/en-us/graph/api/resources/onpremisesextensionattributes?view=graph-rest-1.0"
  target="_parent">onPremisesExtensionAttributes</a></td>
  <td class=xl70 style='font-size:11.0pt;color:#467886;font-weight:400;
  text-decoration:underline;text-underline-style:single;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;border-top:.5pt solid black;
  border-right:.5pt solid black;border-bottom:none;border-left:none'><a
  href="https://learn.microsoft.com/en-us/exchange/recipients/mailbox-custom-attributes"
  target="_parent">Custom attributes in Exchange Server</a></td>
 </tr>
 <tr height=39 style='height:29.0pt'>
  <td height=39 class=xl74 align=left width=283 style='height:29.0pt;
  width:212pt;font-size:14.0pt;color:#467886;font-weight:700;text-decoration:
  underline;text-underline-style:single;text-line-through:none;font-family:
  "Aptos Narrow", sans-serif;border-top:.5pt solid black;border-right:1.0pt solid #A3A3A3;
  border-bottom:1.0pt solid #A3A3A3;border-left:1.0pt solid #A3A3A3'><a
  href="https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#directory-microsoft-entra-id-extensions"
  target="_parent"><span style='font-size:14.0pt;font-weight:700'>Directory
  Extensions</span></a></td>
  <td class=xl66 align=left width=237 style='width:178pt;font-size:11.0pt;
  color:black;font-weight:400;text-decoration:none;text-underline-style:none;
  text-line-through:none;font-family:"Aptos Narrow", sans-serif;border-top:
  .5pt solid black;border-right:none;border-bottom:none;border-left:none'>Custom
  Extension Attributes in Azure AD/Entra ID</td>
  <td class=xl66 align=left width=237 style='width:178pt;font-size:11.0pt;
  color:black;font-weight:400;text-decoration:none;text-underline-style:none;
  text-line-through:none;font-family:"Aptos Narrow", sans-serif;border-top:
  .5pt solid black;border-right:.5pt solid black;border-bottom:none;border-left:
  none'>Azure AD/Entra ID Connect Sync Directory Extensions</td>
 </tr>
 <tr height=25 style='height:18.7pt'>
  <td height=25 class=xl75 align=left width=283 style='height:18.7pt;
  border-top:none;width:212pt;font-size:14.0pt;color:#467886;font-weight:700;
  text-decoration:underline;text-underline-style:single;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;border:1.0pt solid #A3A3A3'><a
  href="https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#schema-extensions"
  target="_parent"><span style='font-size:14.0pt;font-weight:700'>Schema
  Extensions</span></a></td>
  <td class=xl72 align=left style='font-size:11.0pt;color:#467886;font-weight:
  400;text-decoration:underline;text-underline-style:single;text-line-through:
  none;font-family:"Aptos Narrow", sans-serif;border-top:.5pt solid black;
  border-right:none;border-bottom:none;border-left:none'><a
  href="https://learn.microsoft.com/en-us/graph/api/resources/schemaextension"
  target="_parent">Microsoft Graph schema extensions<span
  style='mso-spacerun:yes'> </span></a></td>
  <td style='font-size:11.0pt;color:black;font-weight:400;text-decoration:none;
  text-underline-style:none;text-line-through:none;font-family:"Aptos Narrow", sans-serif;
  border-top:.5pt solid black;border-right:.5pt solid black;border-bottom:none;
  border-left:none'></td>
 </tr>
 <tr height=25 style='height:18.7pt'>
  <td height=25 class=xl75 align=left width=283 style='height:18.7pt;
  border-top:none;width:212pt;font-size:14.0pt;color:#467886;font-weight:700;
  text-decoration:underline;text-underline-style:single;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;border:1.0pt solid #A3A3A3'><a
  href="https://learn.microsoft.com/en-us/graph/extensibility-overview?tabs=http#open-extensions"
  target="_parent"><span style='font-size:14.0pt;font-weight:700'>Open
  Extensions</span></a></td>
  <td class=xl72 align=left style='font-size:11.0pt;color:#467886;font-weight:
  400;text-decoration:underline;text-underline-style:single;text-line-through:
  none;font-family:"Aptos Narrow", sans-serif;border-top:.5pt solid black;
  border-right:none;border-bottom:none;border-left:none'><a
  href="https://learn.microsoft.com/en-us/graph/api/resources/opentypeextension?view=graph-rest-1.0"
  target="_parent">openTypeExtension</a></td>
  <td style='font-size:11.0pt;color:black;font-weight:400;text-decoration:none;
  text-underline-style:none;text-line-through:none;font-family:"Aptos Narrow", sans-serif;
  border-top:.5pt solid black;border-right:.5pt solid black;border-bottom:none;
  border-left:none'></td>
 </tr>
 <tr height=25 style='height:18.7pt'>
  <td height=25 class=xl75 align=left width=283 style='height:18.7pt;
  border-top:none;width:212pt;font-size:14.0pt;color:#467886;font-weight:700;
  text-decoration:underline;text-underline-style:single;text-line-through:none;
  font-family:"Aptos Narrow", sans-serif;border:1.0pt solid #A3A3A3'><a
  href="https://learn.microsoft.com/en-us/entra/fundamentals/custom-security-attributes-overview"
  target="_parent"><span style='font-size:14.0pt;font-weight:700'>Custom
  Security Attributes</span></a></td>
  <td style='font-size:11.0pt;color:black;font-weight:400;text-decoration:none;
  text-underline-style:none;text-line-through:none;font-family:"Aptos Narrow", sans-serif;
  border-top:.5pt solid black;border-right:none;border-bottom:.5pt solid black;
  border-left:none'></td>
  <td style='font-size:11.0pt;color:black;font-weight:400;text-decoration:none;
  text-underline-style:none;text-line-through:none;font-family:"Aptos Narrow", sans-serif;
  border-top:.5pt solid black;border-right:.5pt solid black;border-bottom:.5pt solid black;
  border-left:none'></td>
 </tr>
 <![if supportMisalignedColumns]>
 <tr height=0 style='display:none'>
  <td width=283 style='width:212pt'></td>
  <td width=237 style='width:178pt'></td>
  <td width=237 style='width:178pt'></td>
 </tr>
 <![endif]>
</table>

