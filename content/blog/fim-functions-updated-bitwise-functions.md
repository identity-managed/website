---
title: 'FIM Functions Updated, Bitwise Functions'
date: 2013-04-12T10:46:00.001-07:00
draft: false
url: /2013/04/fim-functions-updated-bitwise-functions.html
tags: 
- Forefront Identity Manager
- FIM 2010 R2
- FIM
---

In addition to the [official reference for functions](http://technet.microsoft.com/en-us/library/ff800820(WS.10).aspx) I thought I would update [my examples from back in the ILM 2 Beta days](http://blog.ilmbestpractices.com/2009/01/ilm-2-functions-explained.html)

**Function Name**

**BitAnd**

Parameters

1) **mask** Type: Integer  
  
2) **flag** Type: Integer

Description

BitAnd is a bitwise operation anding **mask** and **flag**. So if **Flag** is the UserAccountControl Attribute in AD and **mask** is **\-3  
**(the 64-bit [two's complement](http://mathforum.org/library/drmath/view/54344.html) of 2) Then the result is that the disable bit (bit 2) is turned off leaving all of the other bits unchanged.  
  
To figure out what mask to use to turn off a bit multiply that number by negative 1 and then subtract one. To turn off bit 2 and the userAccountControl with -3. To turn off bit 16 -- account is locked out and it with a -17.

Examples

BitAnd(**\-3**, userAccountControl)   
  
Turn off the disable bit Flow the result into [userAccountControl](http://msdn.microsoft.com/en-us/library/ms680832(VS.85).aspx) in AD to enable a user.

 

BitAnd(-3, 514) =512  
  
if userAccountControl is 514 then the example gives us 512, which reactivates an account

 

BitAnd(-3, 512) =512  
  
if it is 512 then it remains unchanged. The account was already active

 

BitAnd(-17, 528) =512  
A locked out account (the bit in the 16's place was on) was unlocked  

 

BitAnd(-17, 512) =512  
An account that was already unlocked was guaranteed to be unlocked  

 

Eq( BitAnd(2,userAccountControl),2)  
This is a test to see if an account in AD is currently disabled.  If so it will return a true otherwise it will return a false.

**Function Name**

**BitOr**

Parameters

1) **mask** Type: Integer  
  
2) **flag** Type: Integer

Description

BitOr is a bitwise operation ORing **mask** and **flag**. So if **Flag** is the UserAccountControl Attribute in AD and **mask** is 2 Then the result is that the disable bit is turned on

Examples

BitOr(2, userAccountControl)  
Turn on the disable bit. Flow the result into userAccountControl in AD to disable a user.  

 

BitOr(2, 512) = 514  
if userAccountControl is 512 then the example gives us 514.  

 

BitOr(2, 514) = 514  
if it is 514 then it remains unchanged.

Hopefully this helps you in your codeless provisioning quest.

Remember there are limitations like the output of IIF can't feed into a function parameter expecting an Integer like the mask or the flag in BitAND or BitOR -- and no, I am not BitOr about it. Without casting and conversion functions that is an obstacle that can't be overcome using the FIM functions for that you may need to turn to [custom workflows](http://www.identitychaos.com/2008/12/ilm-2-rc0-workflow-activity-walkthrough.html).

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices