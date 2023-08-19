---
title: 'ILM 2 Beta 3 Bug: Action Process Function Evaluator Activity doesn''t work when using only one field'
date: 2008-09-12T02:52:00.001-07:00
draft: false
url: /2008/09/ilm-2-beta-3-bug-action-process.html
tags: 
- ILM 2 Beta 3
---

[ID: 367381](https://connect.microsoft.com/feedback/ViewFeedback.aspx?FeedbackID=367381&SiteID=433)

* * *

Description

Action Process Function Evaluator Activity doesn't work when using only one field, but when I concatenate with 2 it works.

**Repro Steps**

Create an action Process  
Add one activity -- Function Evaluator  
Set a destination to an attribute (like DisplayName) and select only one field in the value -- LastName  
Then build an MPR to apply to All People (don't check Grants Permission), Operations: Create and Modify  
Requestors: All People  
All Attributes  
Condition Before All People  
Condition After All People  
Policy Workflows: Add your Action Process  
Then create or modify a user  
open the user again and note that it did not work  
Then look at search requests, view the request and note the following error: Data at the root level is invalid. Line 1, position 1.

This fails

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/ILM2Beta3BugActionProcessFunctionEvaluat_27E5/image_thumb.png)](http://www.ilmbestpractices.com/blog/uploaded_images/ILM2Beta3BugActionProcessFunctionEvaluat_27E5/image.png)

and when used gives this error:

[![clip_image001](http://www.ilmbestpractices.com/blog/uploaded_images/ILM2Beta3BugActionProcessFunctionEvaluat_27E5/clip_image001_thumb.png)](http://www.ilmbestpractices.com/blog/uploaded_images/ILM2Beta3BugActionProcessFunctionEvaluat_27E5/clip_image001.png)

But this works (as does concatenating with a "" string)

[![clip_image001[7]](http://www.ilmbestpractices.com/blog/uploaded_images/ILM2Beta3BugActionProcessFunctionEvaluat_27E5/clip_image0017_thumb.png)](http://www.ilmbestpractices.com/blog/uploaded_images/ILM2Beta3BugActionProcessFunctionEvaluat_27E5/clip_image0017.png)

Please repro and validate as a bug

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices