---
title: 'MS13-066 causes ADFS 2.0 problems'
date: 2013-08-15T08:55:00.001-07:00
draft: false
url: /2013/08/ms13-066-causes-adfs-20-problems.html
---

Microsoft put out a release day before yesterday (8/13/13) to fix a security vulnerability in ADFS 2.0

It caused an outage for SSO with Office365 for a customer of ours (they had the servers set to auto update).

[http://technet.microsoft.com/en-us/security/bulletin/ms13-066](http://technet.microsoft.com/en-us/security/bulletin/ms13-066)

[http://support.microsoft.com/kb/2843639](http://support.microsoft.com/kb/2843639)

[http://support.microsoft.com/kb/2843638](http://support.microsoft.com/kb/2843638)

At the moment we recommend NOT installing these updates.

We saw the following error repeated for every authentication attempt:

Event ID 111 Federation service encountered an error while processing the ws-trust request.

Exception Details:

System.Reflection.TargetInvocationException: Exception has been thrown by the target of an invocation ---> System.TypeLoadException: Could not load type 'Microsoft.IdentityModel.Protocols.XmlSignature.AsymmetricSignatureOperatorsDelegate' from assembly 'Microsoft.IdentityModel, Version=3.5.0.0

It goes on with the stack trace.

Uninstalling these updates has partially restored service: Outlook and Lync now work, but the Outlook Web Access and SharePoint online still aren't working.

In fact they pulled the patch later in the day yesterday.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices