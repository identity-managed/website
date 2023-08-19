---
title: 'RCDC Editor'
date: 2011-06-17T06:58:00.001-07:00
draft: false
url: /2011/06/rcdc-editor.html
tags: 
- Forefront Identity Manager
- FIM
---

[As previously discussed the RCDC](http://blog.ilmbestpractices.com/2009/11/fim-rcdc-explained-in-brief.html) is a very powerful tool for customizing FIM without writing your own front-end and web client. There are several drawbacks to the RCDC. The worst is that you have to export the RCDC to an xml file, open it up in your favorite XML editor, modify it by hand, load it back into the FIM Portal and then run iisreset. All of which means that mistakes are quite painful, as it can take you several minutes to discover your mistake. Worse if you made more than one change. Ugh!  
So thanks to my friends over at OCG there is an [RCDC editor](https://oxfordcomputertraining.com/tools/rcdc-editor/). While not perfect it can shave hours off your time to edit RCDC’s.  
You get an almost WYSIWYG editor that saves you from making many easy simple mistakes. If I need to tweak something simple I might for go it, but then again I have lots of experience tweaking the RCDC by hand (painful experience). For $775 for a project I can get an editor that makes life much simpler. No brainer!  
The UI is good but not perfectly intuitive. I found several “bugs” only to discover that I needed to learn just a bit more about the tool.  
You will need to run a PowerShell command to export the FIM Configuration, install the software before you can use it at all. After activating the license you can save the RCDC’s as XML. Then yes you still have to load the RCDC manually and run iisreset. Nonetheless, this is still much easier.  
While you are still learning more about what the RCDC can do, this is still an iterative process. Creating an RCDC for a new FIM resource type is now a 2-8 hour job instead of 8-32 hour job.  
The Resultant Rights Editor is a nice bonus that allows you to setup scenarios (who is accessing what resource and which attributes to include) so that you can see what control will be visible, and enabled for the different users.  
[![image](http://www.ilmbestpractices.com/blog/uploaded_images/RCDC-Editor_A2C7/image_thumb.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/RCDC-Editor_A2C7/image.png)  
Three complaints (with paraphrased responses from Tools4FIM):  
1) When I purchased the tool the purchase was for a 1 year license – I wasn’t warned anywhere that this was only for a 1 year license until I was completing the purchase. I didn’t spot it in the EULA when I installed the demo version (yes I did read it, if I missed it please let me know). In my opinion, limit the license by time or project, not both. (You get licensed for 1 project – one FIM install, for one year).  
– Apparently, the one year bit is that you only have 1 year to activate the license. You get the license without a time limit. I love it when my complaints are resolved before I make them.  
2) Sometimes I may want to add a control that doesn’t really have anything to do with an attribute, yet the tool forces me to name the control after the attribute.  
\-- Next version (due out Q3) and they intend to allow those that purchase now access to that new version without penalty.  
3) When adding/editing UocDropDownList controls it doesn’t let me set the Caption (what the users sees) for the Option differently than the Value (what the computer sees). It lets me set a hint but not the Caption.  
[![image](http://www.ilmbestpractices.com/blog/uploaded_images/RCDC-Editor_A2C7/image_thumb_3.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/RCDC-Editor_A2C7/image_3.png)  
Yes I did read the help file which tells me that I can do it but not how. So I do think that is a bug.  
\-- Aha! They told me that there is a way to do this. When you modify the Value:  
[![clip_image002](http://www.ilmbestpractices.com/blog/uploaded_images/RCDC-Editor_A2C7/clip_image002_thumb.jpg "clip_image002")](http://www.ilmbestpractices.com/blog/uploaded_images/RCDC-Editor_A2C7/clip_image002.jpg)  
<edited 6/23/2011>  
[![image](http://www.ilmbestpractices.com/blog/uploaded_images/RCDC-Editor_A2C7/image_thumb_6.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/RCDC-Editor_A2C7/image_6.png)  
The Option Value is the value (what the computer will see – SA) and the Constant is the caption that the user will see (Admin Account).  
So it looks like this:  
[![image](http://www.ilmbestpractices.com/blog/uploaded_images/RCDC-Editor_A2C7/image_thumb_7.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/RCDC-Editor_A2C7/image_7.png)  
</edited>  
Wish list:  
1) Copy all of the XML data sources (like regions, or other custom data sources) so that I can manage them centrally and copy them into other RCDC’s. That way if a new country is born tomorrow, or next year, I only have one place to go update the list of countries and their codes instead of in several different RCDC’s for several different resource types.  
2) Let me copy all of the settings from one control to another. Sometimes I want 4 text boxes right after another with all of the same settings, just different binding.  
\-- Next version and they promised to name the feature after me ![Winking smile](http://www.ilmbestpractices.com/blog/uploaded_images/RCDC-Editor_A2C7/wlEmoticon-winkingsmile.png)  
3) XML editor (or link to) so that I can open it up for the manual tweaks that RCDC Editor doesn’t do yet.  
\-- They are thinking about it for the next version.  
4) Add the ability to run the export PowerShell script from the tool (probably also need to let me configure the exact command line).  
\-- Already planning on it in the next version  
5) Add the ability to upload the RCDC right from the tool, optionally running iisreset.  
\-- Already planning on it in the next version  
6) Home Page and Nav Bar editing, especially with the Resultant Rights Evaluator.  
7) FIM Portal style sheet editing  
8) Ability to diffs with previous versions (whether stored by the Editor or by querying the FIM Service for recent requests to modify the RCDC  
**Bottom line: This is a tool that I as a FIM implementer can’t live without**, especially at the $775 price.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices