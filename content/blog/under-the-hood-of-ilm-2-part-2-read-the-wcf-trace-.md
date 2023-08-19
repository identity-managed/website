---
title: 'Under the hood of ILM 2 -- Part 2 Read the WCF Trace!'
date: 2008-11-01T10:01:00.001-07:00
draft: false
url: /2008/11/under-hood-of-ilm-2-part-2-read-wcf.html
tags: 
- ILM
- ILM 2 Beta 3
- WCF
---

Take a look at [Part 1 to enable tracing](/blog/2008/11/under-hood-of-ilm-2-part-1-enable-wcf.html)

To view the log you need to have installed the Windows SDK and then you use the Service Trace Viewer

C:\\Program Files\\Microsoft SDKs\\Windows\\v6.0A\\Bin\\SvcTraceViewer.exe

If the file is over 50 MB you will get the partial loading screen like this one. Try and limited the estimated size, if you open too much it will be very slow. Even 20 MB can be really slow.

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/UnderthehoodofILM2Part2ReadtheWCFTrace_83B2/image_thumb.png)](http://www.ilmbestpractices.com/blog/uploaded_images/UnderthehoodofILM2Part2ReadtheWCFTrace_83B2/image.png)

If you need to adjust this after you open the file you can

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/UnderthehoodofILM2Part2ReadtheWCFTrace_83B2/image_thumb_3.png)](http://www.ilmbestpractices.com/blog/uploaded_images/UnderthehoodofILM2Part2ReadtheWCFTrace_83B2/image_3.png)

To view what is happening you click on Activity 00000000000000 and then browse through the  actions

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/UnderthehoodofILM2Part2ReadtheWCFTrace_83B2/image_thumb_4.png)](http://www.ilmbestpractices.com/blog/uploaded_images/UnderthehoodofILM2Part2ReadtheWCFTrace_83B2/image_4.png)

Most of it is just noise -- "The Policy Application Manager is executing" or "The Policy Application Manager has finished executing" (the first two showing below.

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/UnderthehoodofILM2Part2ReadtheWCFTrace_83B2/image_thumb_5.png)](http://www.ilmbestpractices.com/blog/uploaded_images/UnderthehoodofILM2Part2ReadtheWCFTrace_83B2/image_5.png)

Take a look at the next action ExecuteQuery.ExecuteReader where in it is retrieving a list of Workflow Definitions objects (See the detail information where it shows the XPath query filter inside the parenthesis

> Query: QueryProcessor.ExecuteQuery.ExecuteReader(/WorkflowDefinition)

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/UnderthehoodofILM2Part2ReadtheWCFTrace_83B2/image_thumb_6.png)](http://www.ilmbestpractices.com/blog/uploaded_images/UnderthehoodofILM2Part2ReadtheWCFTrace_83B2/image_6.png)

The you can see how it retrieves the objects that were returned as part of the query

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/UnderthehoodofILM2Part2ReadtheWCFTrace_83B2/image_thumb_7.png)](http://www.ilmbestpractices.com/blog/uploaded_images/UnderthehoodofILM2Part2ReadtheWCFTrace_83B2/image_7.png)

The process continues to retrieve objects and then sets up a WorkflowServiceHost for the workflows

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/UnderthehoodofILM2Part2ReadtheWCFTrace_83B2/image_thumb_8.png)](http://www.ilmbestpractices.com/blog/uploaded_images/UnderthehoodofILM2Part2ReadtheWCFTrace_83B2/image_8.png)

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices