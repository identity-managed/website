---
title: 'The attributes behind Message Delivery Restrictions'
date: 2009-06-29T00:40:00.000-07:00
draft: false
url: /2009/06/attributes-behind-message-delivery.html
tags: 
- MIIs
- ILM
- Exchange 2007
- FIM
---

Do you know what attributes are used to control who can and can't send to a Distribution List in Exchange 2003 and Exchange 2007? or Does it use a DACL?

Knowing such things is key if you are going to automate distribution list management through .NET programs, or MIIS/ILM/FIM, Quest ARS or any other tool that is talking to LDAP attributes. For Powershell you need a separate list since the names are different.

Seeing as how a picture is worth a thousand words I'll include some after a brief explanation:

At first I was afraid that it used the SendTo permission on DACLs but fortunately that is not what the Exchange GUI tools change. This is fortunate since ILM does not have an out of the box MA that modifies DACLs on AD objects, it is also fortunate since programming against DACLs is somewhat complicated. I must give thanks to my friend [Joe Kaplan](http://www.joekaplan.net/) and his co-author Ryan Dunn for the helps in their book (see page 302 listing 8.2 listing the DACL) and their forum [http://directoryprogramming.net/default.aspx](http://directoryprogramming.net/default.aspx "http://directoryprogramming.net/default.aspx")

[The .NET Developer's Guide to Directory Services Programming](http://www.amazon.com/Developers-Directory-Programming-Microsoft-Development/dp/0321350170/ref=sr_1_1?ie=UTF8&s=books&qid=1246251608&sr=8-1)

With the help from their book I was able to eliminate DACLs since the darn things never changed. FC never lies.

Open the Exchange Console, navigate to the Distribution lists open their properties and go to Mail Flow Settings click on Message Delivery Restrictions and then click on the Blue check mark next to Properties:

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/TheattributesbehindMessageDeliveryRestri_132C9/image_thumb.png)](http://www.ilmbestpractices.com/blog/uploaded_images/TheattributesbehindMessageDeliveryRestri_132C9/image.png)

So what I found was five attributes that control the fate of who can and who can't send to a particular recipient (in this case a distribution list)

authOrig, unauthOrig, and msExchRequireAuthToSendTo,

Attribute Name

Name in GUI

Explanation

[Powershell (Set-DistributionGroup)](http://technet.microsoft.com/en-us/library/bb124955.aspx)   
Just as an FYI

authOrig

Accept messages from  
Only senders in the following list:

If this attribute and dLMemSubmitPerms are both empty then that is the equivalent of All Senders. If populated only those recipients and the members of Distribution Lists enumerated in dLMemSubmitPerms can sends listed can send items to this distribution list minus anyone listed in unauthOrig and anyone that is a member of distribution lists enumerated in dLMemRejectPerms

\-AcceptMessagesOnlyFrom

dLMemSubmitPerms

same as above

see above

\-AcceptMessagesOnlyFromDLMembers

unauthOrig

Reject messages from  
Senders in the following list:

Prevents recipients listed here from sending to this Distribution list

\-RejectMessagesFrom

dLMemRejectPerms

same as above

Prevents recipients who are members of the Distribution lists mentioned from sending email to this Distribution list

\-RejectMessagesFromDLMembers

msExchRequireAuthToSendTo

Require that all senders are authenticated

When set to True only authenticated users (no external users) can send mail to this Distribution list

\-RequireAllSendersAreAuthenticated

For more info on attribute to Powershell attribute name conversions see

[http://blogs.technet.com/evand/archive/2007/02/19/filterable-properties-in-exchange-2007-rtm.aspx](http://blogs.technet.com/evand/archive/2007/02/19/filterable-properties-in-exchange-2007-rtm.aspx "http://blogs.technet.com/evand/archive/2007/02/19/filterable-properties-in-exchange-2007-rtm.aspx")

For more on the Powershell commands with some examples see

[http://technet.microsoft.com/en-us/library/bb397214.aspx](http://technet.microsoft.com/en-us/library/bb397214.aspx "http://technet.microsoft.com/en-us/library/bb397214.aspx")

What would be really nice would be if FIM 2010 already had the schema and OVC extended for this. Since this is the very next thing people at a big company ask for after finding out they can automate distribution list maintenance.

As promised some pretty pictures to help explain (on the left you see the screenshot from ADSI edit and on the right the snapshot of the Exchange Console

[![authOrig](http://www.ilmbestpractices.com/blog/uploaded_images/TheattributesbehindMessageDeliveryRestri_132C9/image_thumb_3.png)](http://www.ilmbestpractices.com/blog/uploaded_images/TheattributesbehindMessageDeliveryRestri_132C9/image_3.png)

[![dLMemSubmitPerms](http://www.ilmbestpractices.com/blog/uploaded_images/TheattributesbehindMessageDeliveryRestri_132C9/image_thumb_4.png)](http://www.ilmbestpractices.com/blog/uploaded_images/TheattributesbehindMessageDeliveryRestri_132C9/image_4.png)

On this one I reverse the order

[![unauthOrig](http://www.ilmbestpractices.com/blog/uploaded_images/TheattributesbehindMessageDeliveryRestri_132C9/image_thumb_5.png)](http://www.ilmbestpractices.com/blog/uploaded_images/TheattributesbehindMessageDeliveryRestri_132C9/image_5.png)

By now you get the idea, that if you select a distribution listt in the Senders in the following list they get put here:

[![dLMemRejectPerms](http://www.ilmbestpractices.com/blog/uploaded_images/TheattributesbehindMessageDeliveryRestri_132C9/image_thumb_6.png)](http://www.ilmbestpractices.com/blog/uploaded_images/TheattributesbehindMessageDeliveryRestri_132C9/image_6.png)

So we see that the Exchange Console clever sorts the DLs from the individuals and puts them into their separate attributes.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices