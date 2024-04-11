---
title: SSL v TLS with EntraID Sync and MIM's Generic LDAP Connector
description: SSL v TLS with EntraID Sync and MIM's Generic LDAP Connector
tags:
  - MIM;EntraIDSync
categories: []
date: 2024-04-11T05:53:35.659Z
banner: /img/tls-authentication-options.png
---
Everyone knows that SSL is vulnerable and we should therefore use TLS. What isn't well understood is the options presented for Binding (authentication) when using the Generic LDAP Connector with AADConnect or the Generic LDAP ECMA 2.x  with MIM.

We are presented 5 options:

* Anonymous
* Basic
* Kerberos
* SSL
* TLS

![Generic LDAP Authentication Options](/img/tls-authentication-options.png "Generic LDAP Authentication Options")

When we tested we could get the SSL option to work over port 636, and we could get the TLS option to work on port 389 but we couldn't get the TLS option to work over port 636. Using a protocol analyzer we confirmed that both ways were using TLS 1.2.

Some web searching turned up the following on the [`website doc of a competing Identity product on how they connect`](https://support.oneidentity.com/technical-documents/identity-manager/8.1.2/administration-guide-for-connecting-to-ldap/34>)to LDAP:

* U﻿se SSL

  * SSL/TLS encrypted is used to establish a connection. Variable: CP_UseSsl
* U﻿se StartTLS

  * S﻿tartTLS is used for encryption. Variable: CP_UseStartTls

So it occurred to me that SSL really means SSL/TLS and that TLS really means StartTLS.

So then I started [reading about StartTLS vs LDAPS](https://www.php.net/manual/en/function.ldap-start-tls.php):

> Please note there is a difference between ldaps and start-TLS for ldap.  start-TLS uses port 389, while ldaps uses port 636.  ldaps has been deprecated in favour of start-TLS for ldap.  Both encrypted (start-TLS ldap)  and unencrypted ldap (ldap) run on port 389 concurrently.
>
> Errors encountered are generally due to misunderstanding how to implement TLS-encrypted ldap

There is a clue to this is in the [LDAP Connector doc](https://docs.microsoft.com/en-us/microsoft-identity-manager/reference/microsoft-identity-manager-2016-connector-genericldap):

> The connector uses the port number specified in the configuration, which by default is 389 for LDAP and 636 for LDAPS.
>
> For LDAPS, you must use SSL 3.0 or TLS. SSL 2.0 is not supported and cannot be activated.

So the last two options should really be labelled:

* SSL/TLS --SSL/TLS depending on what your server is configured to use 
* StartTLS --  talk over the normally unecrypted port and then use StartTLS to encrypt everything.