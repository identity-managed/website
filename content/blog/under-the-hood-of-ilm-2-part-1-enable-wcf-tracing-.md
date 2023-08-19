---
title: 'Under the hood of ILM 2 -- Part 1 Enable WCF Tracing!'
date: 2008-11-01T09:23:00.001-07:00
draft: false
url: /2008/11/under-hood-of-ilm-2-part-1-enable-wcf.html
tags: 
- ILM
- ILM 2 Beta 3
- WCF
---

Want to understand what is happening with your custom ILM 2 workflow? or your calls to the web service?

Try enabling WCF Tracing. By enabling WCF tracing for the Identity Lifecycle Manager Resource Management Service you get to track requests to the webservice. This can help you figure out if your requests are even getting to the webservice.

To enable tracing open the config file:

C:\\Program Files\\Microsoft Identity Management\\Common Services\\

Microsoft.ResourceManagement.Service.exe.config

In the <configuration> after </configsections> and before <appsettings> add the following:

```
<!-- Enable Tracing -->  
  <system.diagnostics\>  
    <trace autoflush\="true" />  
    <sources\>  
      <source name\="Microsoft.ResourceManagement" switchValue\="All"\>  
        <listeners\>  
          <add name\="text" type\="System.Diagnostics.TextWriterTraceListener" initializeData\="c:\\logs\\service.txt" traceOutputOptions\="Timestamp,ThreadId,DateTime"/>  
          <add name\="xml" type\="System.Diagnostics.XmlWriterTraceListener" initializeData\="c:\\logs\\service.svclog" traceOutputOptions\="Timestamp,ThreadId,DateTime"/>  
        </listeners\>  
      </source\>  
    </sources\>  
  </system.diagnostics\>  
  <!-- End Enable Tracing -->
```  
<br /><br /><br />.csharpcode, .csharpcode pre<br />{<br /> font-size: small;<br /> color: black;<br /> font-family: consolas, "Courier New", courier, monospace;<br /> background-color: #ffffff;<br /> /\*white-space: pre;\*/<br />}<br />.csharpcode pre { margin: 0em; }<br />.csharpcode .rem { color: #008000; }<br />.csharpcode .kwrd { color: #0000ff; }<br />.csharpcode .str { color: #006080; }<br />.csharpcode .op { color: #0000c0; }<br />.csharpcode .preproc { color: #cc6633; }<br />.csharpcode .asp { background-color: #ffff00; }<br />.csharpcode .html { color: #800000; }<br />.csharpcode .attr { color: #ff0000; }<br />.csharpcode .alt <br />{<br /> background-color: #f4f4f4;<br /> width: 100%;<br /> margin: 0em;<br />}<br />.csharpcode .lnum { color: #606060; }  
  

Then you need to create a directory called c:\\ILMLogs and restart the ILM Common Services. If you don't create the directory then the logging still won't work, and you'll have to restart the service.

  
  

To view the log you need to have installed the Windows SDK and then you use the Service Trace Viewer

  
  

C:\\Program Files\\Microsoft SDKs\\Windows\\v6.0A\\Bin\\SvcTraceViewer.exe

  
  

[For more info on how to read and interpret the trace see Part 2.](/blog/2008/11/under-hood-of-ilm-2-part-2-read-wcf.html)

  
  

For more info on writing your own traces from your own code see [Craig Martin's post on WCF tracing.](http://miisexperts.org/craigm/2008/06/over-communicate.html)

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices