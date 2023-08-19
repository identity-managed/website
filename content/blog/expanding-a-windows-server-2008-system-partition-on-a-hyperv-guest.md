---
title: 'Expanding a Windows Server 2008 System partition on a HyperV Guest'
date: 2008-09-02T19:47:00.001-07:00
draft: false
url: /2008/09/expanding-windows-server-2008-system.html
tags: 
- HyperV
- ILM 2 Beta 3
- Windows Server 2008
---

While building out some virtual machines for our ILM 2 Beta 3 environment...

We setup a few virtual machines 64 bit Windows Server 2008 SP 1 (since SP 1 is built in to the RTM) running on HyperV. Everything is very slick! Except we only set aside 16 GB for the virtual disk for the system partition. Despite installing SQL, SharePoint, and ILM 2 to another drive the system partition quickly filled up, and didn't have enough room for Visual Studio (even though I wanted to install it on another partition). All of these programs install a lot of stuff on the system partition no matter what I select. While moving the paging file freed up some space it wasn't enough.

Then of course someone went and reread the [Windows Server 2008 requirements](http://msdn.microsoft.com/en-us/windowsserver/cc196364.aspx) and they said minimum 10 GB recommended 40 GB. So we decided to go for 64 GB. But expanding your system partition is not all that straightforward.

Here is how:

4:21 PM

If the virtual disk needs to be expanded you need to ensure that there are no snapshots and that it is shutdown. If there are snapshots you will need to delete them. This deletion will require a disk merge to take place and will take a while

[![clip_image001](http://www.ilmbestpractices.com/blog/uploaded_images/ExpandingaWindowsServer2008Systempartiti_104BD/clip_image001_thumb.png)](http://www.ilmbestpractices.com/blog/uploaded_images/ExpandingaWindowsServer2008Systempartiti_104BD/clip_image001.png)

Highlight the VM and click settings

Navigate to the Hard drive you wish to expand

[![clip_image001[4]](http://www.ilmbestpractices.com/blog/uploaded_images/ExpandingaWindowsServer2008Systempartiti_104BD/clip_image0014_thumb.png)](http://www.ilmbestpractices.com/blog/uploaded_images/ExpandingaWindowsServer2008Systempartiti_104BD/clip_image0014.png)

Then click Edit. On the choose action screen select expand. (if this is a fixed disk then you will need to do a convert)

[![clip_image001[6]](http://www.ilmbestpractices.com/blog/uploaded_images/ExpandingaWindowsServer2008Systempartiti_104BD/clip_image0016_thumb.png)](http://www.ilmbestpractices.com/blog/uploaded_images/ExpandingaWindowsServer2008Systempartiti_104BD/clip_image0016.png)

Enter the new size and click finish Then wait a while

[![clip_image001[8]](http://www.ilmbestpractices.com/blog/uploaded_images/ExpandingaWindowsServer2008Systempartiti_104BD/clip_image0018_thumb.png)](http://www.ilmbestpractices.com/blog/uploaded_images/ExpandingaWindowsServer2008Systempartiti_104BD/clip_image0018.png)

Next configure the VM to boot from CD/DVD

Configure the DVD to use a windows server 2008 WinPE iso image

Which can be obtained from here by downloading

[http://www.microsoft.com/downloads/details.aspx?familyid=94BB6E34-D890-4932-81A5-5B50C657DE08&displaylang=en](http://www.microsoft.com/downloads/details.aspx?familyid=94BB6E34-D890-4932-81A5-5B50C657DE08&displaylang=en)

[![clip_image001[10]](http://www.ilmbestpractices.com/blog/uploaded_images/ExpandingaWindowsServer2008Systempartiti_104BD/clip_image00110_thumb.png)](http://www.ilmbestpractices.com/blog/uploaded_images/ExpandingaWindowsServer2008Systempartiti_104BD/clip_image00110.png)

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/ExpandingaWindowsServer2008Systempartiti_104BD/image_thumb.png)](http://www.ilmbestpractices.com/blog/uploaded_images/ExpandingaWindowsServer2008Systempartiti_104BD/image.png)

Before starting the VM realize that you only have a short window to tell it to boot from CD/DVD

So Connect to the VM before you turn it on

[![clip_image001[12]](http://www.ilmbestpractices.com/blog/uploaded_images/ExpandingaWindowsServer2008Systempartiti_104BD/clip_image00112_thumb.png)](http://www.ilmbestpractices.com/blog/uploaded_images/ExpandingaWindowsServer2008Systempartiti_104BD/clip_image00112.png)

Within a few seconds it will prompt you to click any key to boot from cd or dvd

Then windows files will load if you are prompted to press ctrl alt delete then it didn't work shut down and try again

If you see this then you are successful. Wait another few seconds for the prompt to appear

[![clip_image001[14]](http://www.ilmbestpractices.com/blog/uploaded_images/ExpandingaWindowsServer2008Systempartiti_104BD/clip_image00114_thumb.png)](http://www.ilmbestpractices.com/blog/uploaded_images/ExpandingaWindowsServer2008Systempartiti_104BD/clip_image00114.png)

Enter DiskPart by typing DiskPart at the command prompt

[![clip_image001[16]](http://www.ilmbestpractices.com/blog/uploaded_images/ExpandingaWindowsServer2008Systempartiti_104BD/clip_image00116_thumb.png)](http://www.ilmbestpractices.com/blog/uploaded_images/ExpandingaWindowsServer2008Systempartiti_104BD/clip_image00116.png)

Select the disk you want (select disk 0) and confirm by typing detail disk

If you need help type list disk

Next select the right volume (select volume 1)

[![clip_image001[18]](http://www.ilmbestpractices.com/blog/uploaded_images/ExpandingaWindowsServer2008Systempartiti_104BD/clip_image00118_thumb.png)](http://www.ilmbestpractices.com/blog/uploaded_images/ExpandingaWindowsServer2008Systempartiti_104BD/clip_image00118.png)

Then expand the volume by entering in how much larger to make it -- not the new size, but the difference between the current size and the new size

[![clip_image001[20]](http://www.ilmbestpractices.com/blog/uploaded_images/ExpandingaWindowsServer2008Systempartiti_104BD/clip_image00120_thumb.png)](http://www.ilmbestpractices.com/blog/uploaded_images/ExpandingaWindowsServer2008Systempartiti_104BD/clip_image00120.png)

Then reboot by typing exit then hitting enter, twice (once to leave bootpart and then once to leave the WPE)

(If you want you can also change your boot order as this will eliminate a small delay in the boot process)

Then log on and confirm it is done

[![clip_image002](http://www.ilmbestpractices.com/blog/uploaded_images/ExpandingaWindowsServer2008Systempartiti_104BD/clip_image002_thumb.png)](http://www.ilmbestpractices.com/blog/uploaded_images/ExpandingaWindowsServer2008Systempartiti_104BD/clip_image002.png)

While I had fun uncovering the secrets of HyperV (thanks to Ian Henry for teaching me about [WPE](http://en.wikipedia.org/wiki/Windows_Preinstallation_Environment)), the most valuable thing I did today was to play tee-ball and soccer with my eight year old daughter and my three sons.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices