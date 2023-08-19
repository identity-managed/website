---
title: 'Love One Note -- hate KB''s with unintended consequences'
date: 2008-08-16T09:44:00.001-07:00
draft: false
url: /2008/08/love-one-note-hate-office-diagnostics.html
---

I love One Note. Especially on a tablet PC. I can take notes either by typing or writing on the screen, I can sign contracts it is great.

We recently purchased a home. My real estate agent would send me documents, I would print to One Note and then sign them, print to PDF using Primo PDF and send them back.

It was great until Print to One Note stopped working. The Send to One Note 2007 printer was gone. My old Send to One note 2003 (BC) was still there but of course could not work. So I followed a KB article and created the printer by hand, and could not get it to work.

So after 3 fruitless attempts, I ran Office Diagnostics in One Note 2007. After 3 fruitless attempts, I ran Office Repair. After 3 fruitless attempts (notice a pattern here), I opened PowerPoint and discovered the following:

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/LoveOneNotehateOfficeDiagnosticsandRepai_14DE/image_thumb.png)](http://www.ilmbestpractices.com/blog/uploaded_images/LoveOneNotehateOfficeDiagnosticsandRepai_14DE/image.png)

I can't read the text of any PowerPoint file. Pictures show up fine, but the text is all garbled. It does not matter what font I select.

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/LoveOneNotehateOfficeDiagnosticsandRepai_14DE/image_thumb_3.png)](http://www.ilmbestpractices.com/blog/uploaded_images/LoveOneNotehateOfficeDiagnosticsandRepai_14DE/image_3.png)

Before burning a ticket with Microsoft on this or uninstalling and reinstalling Office I thought I would post this here and go sprinkle some questions among the PowerPoint newgroups.

**Update as of 8/20/2008**

Some of the Powerpoint MVP's gave me some excellent advice along with a link to an FAQ, that perfectly addressed my problem

[How to install a TEST printer driver(and why PowerPoint is cranky about printers)](http://www.pptfaq.com/FAQ00952.htm "FAQ00952.htm")

I still have my problem with One Note and have opened a ticket on that one:

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/LoveOneNotehateOfficeDiagnosticsandRepai_14DE/image_thumb_4.png)](http://www.ilmbestpractices.com/blog/uploaded_images/LoveOneNotehateOfficeDiagnosticsandRepai_14DE/image_4.png)

I had followed the advice in the following KB article:

[http://kbalertz.com/952216/OneNote-printer-missing-Print-dialog-Office-program.aspx](http://kbalertz.com/952216/OneNote-printer-missing-Print-dialog-Office-program.aspx "http://kbalertz.com/952216/OneNote-printer-missing-Print-dialog-Office-program.aspx")

When I set the manually created Send to One Note 2007 printer to be the default printer (as stated in method 2 of the KB article) that's when I got the PowerPoint text problem.

In the link below the posters said to run Office Diagnostics. Didn't work for me.

[http://www.technologyquestions.com/technology/microsoft-onenote/181259-onenote-2007-printer-missing.html](http://www.technologyquestions.com/technology/microsoft-onenote/181259-onenote-2007-printer-missing.html "http://www.technologyquestions.com/technology/microsoft-onenote/181259-onenote-2007-printer-missing.html")

This link had an interesting idea

[http://www.gottabemobile.com/Where+Is+My+OneNote+2007+Printer.aspx](http://www.gottabemobile.com/Where+Is+My+OneNote+2007+Printer.aspx "http://www.gottabemobile.com/Where+Is+My+OneNote+2007+Printer.aspx")

[http://blogs.msdn.com/descapa/archive/2008/02/06/how-to-fix-missing-printer-icon.aspx](http://blogs.msdn.com/descapa/archive/2008/02/06/how-to-fix-missing-printer-icon.aspx "http://blogs.msdn.com/descapa/archive/2008/02/06/how-to-fix-missing-printer-icon.aspx")

Until I get it fixed my current workarounds are to grab a screen clipping with One Note(much less effective)

Or to use Agilix GoBinder Lite.

**8/22/2008**

According to the tech at MSFT, quickbooks could be the culprit and we both laughed as he told me that the recommended fix was to uninstall Quickbooks. But he softened it to the Quickbooks PDF printer. We sure enough that did it. I deleted the Quickbooks PDF printer and voila the printer came back.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices