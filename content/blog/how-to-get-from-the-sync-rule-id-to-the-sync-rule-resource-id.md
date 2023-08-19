---
title: 'How to get from the Sync-Rule-ID to the Sync Rule Resource ID'
date: 2013-05-01T12:03:00.001-07:00
draft: false
url: /2013/05/how-to-get-from-sync-rule-id-to-sync.html
tags: 
- Forefront Identity Manager
- FIM 2010 R2
- FIM
---

If you are looking at the XML export of the FIM synchronization config and you are trying to track down which sync rule is supplying a particular flow you just need to know which numbers lead you where.

For example:

<import-flows mv-attribute="accountName" type="ranked">  
      <import-flow src-ma="{9686B319-E4BF-49C5-90C9-59054CCE3F92}"  
                   cd-object-type="user" id="{210D4BB7-B886-4898-8361-7A232BBD65E8}">  
        <sync-rule-mapping mapping-type="direct"  
                           **sync-rule-id="{B3E7157E-2EDA-E111-BCF5-005056000006}"  
**                           sync-rule-mapping-id="{52CF9D5C-33C8-4E1F-B56C-C77F7A9A1577}"  
                           initial-flow-only="false" is-existence-test="false">  
          <src-attribute>sAMAccountName</src-attribute>  
        </sync-rule-mapping>  
      </import-flow>  
    </import-flows>

The key to finding the Sync rule is of course the Sync rule ID. However, this is not the resource ID that I can search for in the FIM Portal. Rather this is the metaverse ID.

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/baa99ca3a8e7_9921/image_thumb.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/baa99ca3a8e7_9921/image.png)

From there I can open the list of connectors and for sync rules there should be one -- the FIM MA.

Then I can see the Distinguished Name of the Sync rule which is the Resource ID (aka ObjectID)

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/baa99ca3a8e7_9921/image_thumb_3.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/baa99ca3a8e7_9921/image_3.png)

Then I can search in the FIM Portal by ResourceId and find the corresponding Synchronization rule:

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/baa99ca3a8e7_9921/image_thumb_4.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/baa99ca3a8e7_9921/image_4.png)

Even better is to use the Join-ImportToExportAttributeFlow PowerShell commandlet originally created by Craig Martin [http://fimpowershellmodule.codeplex.com/](http://fimpowershellmodule.codeplex.com/ "http://fimpowershellmodule.codeplex.com/")

Joe Zamora found and tweaked a minor bug in it: [http://c--shark.blogspot.com/2013/03/one-small-addition-to-powershell-module.html](http://c--shark.blogspot.com/2013/03/one-small-addition-to-powershell-module.html "http://c--shark.blogspot.com/2013/03/one-small-addition-to-powershell-module.html") be sure to use this fix.

Using the commandlet you can have a spreadsheet showing you the end to end attribute flow.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices