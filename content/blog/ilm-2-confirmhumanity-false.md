---
title: 'ILM "2" confirmHumanity="false"'
date: 2008-12-23T12:52:00.001-07:00
draft: false
url: /2008/12/ilm-confirmhumanity.html
tags: 
- ILM
- Humor
- ILM 2 RC0
---

I was getting ready to try out some of the various installation topologies that may be possible with ILM "2" including: separating the Portal and the Service (definitely possible), having two portals point back to the same service (I think it's possible), when I came across the most interesting item in the [ILM "2" installation guide](http://technet.microsoft.com/en-us/library/cc561135.aspx) in the section on Installing the ILM Service and ILM Portal on separate servers. Let's see if you can spot it too:

On ILM Service server, edit the file

*   c:\\Program Files\\Microsoft Identity Management\\Common Services\\Microsoft.ResourceManagement.Service.exe.config as follows:
    *   <resourceManagementService certificateName="IdentityLifecycleManager2" **confirmHumanity="false"** servicePrincipalName="IdentityManagementService/_computername_"/>
        

What in the world can that be about? confirmHumanity="false"? Well at least the coder followed camelCasing so we may have a hint as to the perpetrator's identity -- Jerry Camel have you been doing some work for Microsoft?

Will someone please explain what this means? Is ILM "2" the Terminator? I mean it will deactivate and deprovision your accounts when you leave -- and afterwards it can show that you have been terminated!

We may never know! But comments are welcome.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices