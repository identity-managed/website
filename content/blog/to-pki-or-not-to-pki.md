---
title: 'To PKI or not to PKI?'
date: 2009-06-02T11:12:00.001-07:00
draft: false
url: /2009/06/to-pki-or-not-to-pki.html
tags: 
- Forefront Identity Manager
- AD RMS
- ILM
- Certificates
- CLM
- RMS
---

When should one implement a Public Key Infrastructure and when should one not? Obviously we implement a PKI to solve a problem, usually around security, enabling secure communications with a web server, multi-factor authentication, encryption. A PKI solution can be very versatile, but it comes at a price in setup and maintenance. But what alternatives do we have? Let's examine each problem in turn

Problem

PKI difficulties

Alternatives

Benefits for Alternatives

Enable Secure web transactions (SSL)

certs expire without warning anyone

none

 

Secure network communications (IPSEC)

Need to issue certificates to all client computers (can use AutoEnroll GPO)

none

 

Multi-factor authentication for Wireless networks using 802.1X

Need to issue certificates to all client computers or smart cards to all users

Radius -- One Time Password Tokens

With Quest Defender issuing and maintaining of OTP is very easy. Defender is much easier than standing up a PKI and issuing smart cards to everyone

Multi-factor authentication (certificates, smart cards)

Need to issue smart cards to all users (can be time consuming) Need special hardware

One Time Password Tokens

With Quest Defender issuing and maintaining of OTP is very easy. Defender is much easier than standing up a PKI and issuing smart cards to everyone. Can work even on computers without the smart card reader.

Encryption of files (EFS)

Need to issue smart cards to all users (can be time consuming)

AD Rights Management Services

Enrollment of users is transparent -- new users can be given permissions by adding them to groups without having to re-encrypt the files. No need to renew certificates. Restrictions are enforced after file is opened. It allows you to assign rights and permissions to other people to documents (open, saving, edit, print, cut and paste) and emails (forward, cut and paste)

Enabling users (internal and/or external) to use your code without getting scary warning (Signing Code Modules, Macros, ActiveX controls etc)

Need to issue/buy certificates for developers

none

 

Signing emails

Need to issue certificates (whether on smart cards or not) to all users

PGP (web of trust)

 

Encrypting emails

Need to issue certificates (whether on smart cards or not) to all users

AD Rights Management Services  
  
or  
PGP (web of trust)

AD RMS Enrollment of users is transparent. Restrictions are enforced after file is opened. It allows you to assign rights and permissions to other people to documents (open, saving, edit, print, cut and paste) and emails (forward, cut and paste)

In short you need certificates for SSL, IPSEC, code signing and signing emails. Whether you build your own PKI or get certificates for them is another question. For SSL and code signing you can get away with buying your certs and should if your web site and/or code is for the public (although if you have enough you may want to look at setting up a subordinate CA with a Public CA that way you control the certs but they are issued through a trusted root CA and your customer don't get those confidence inspiring messages asking them whether to trust you or not) . For IPSEC and signing emails you should implement your own PKI in order to save the cost of buying so many certs.

If you need to implement signing of emails along with multi-factor authentication then it makes sense to take advantage of the versatility of certificates on smart cards. Then it makes sense to implement the Certificate Management component (CLM) of ILM 2007 to ease many of the challenges with issuing and managing smart cards.

However, if multi-factor authentication and encryption are your main goals you may want to take a look at one time password tokens with Defender and Microsoft's AD Rights Management Services (AD RMS) respectively. Both present easier and perhaps cheaper alternatives, that also add capabilities. Defender adds the capability to use multi-factor authentication on machines without smart card readers, and AD RMS adds the capability to restrict what users can do with content even after they decrypt it.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices