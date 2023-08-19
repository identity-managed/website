---
title: 'ILM 2 Web Services Part 1 The Service Reference'
date: 2008-11-01T10:22:00.001-07:00
draft: false
url: /2008/11/ilm-2-web-services-part-1-service.html
tags: 
- ILM
- Identity Management
- ILM 2 Beta 3
- WCF
- Web Services
---

Together, Mark Struck of Ipseity Inc and I, have figured out (after much beating of our heads against brick walls) how to use the ILM 2 Enumeration Endpoint to perform some basic reporting. (I figured out how to send the enumeration and get a response and then Mark figured out how to correctly form the pull messages so as to be able to retrieve the actual objects -- teamwork at its finest). We would also like to thank Mark Gabarra and Rob Ward for their input.

Here are some lessons we learned:

First lesson: the SDK provided with ILM 2 Beta 3 is incomplete and in some cases misleading. (Just one of those areas that hasn't been well documented yet)

Second lesson: Reading the WS-Enumeration specification is like drinking from a firehouse.

Third lesson: Case matters when specifying the endpoint.

Today's post will show you how to setup the Service Reference.

Type in [http://localhost:526/ResourceManagementService/MEX/](http://localhost:526/ResourceManagementService/MEX/)

The case of the url is important. R M S must be capitals and so must MEX.

The name you type in for name space is important as it is the name you will use in your code.

I recommend replacing the ServiceReference1 that you see in the figure with ILM\_RMS.

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/ILM2WebServicesHowtoactuallyusethem_11C9F/image_thumb.png)](http://www.ilmbestpractices.com/blog/uploaded_images/ILM2WebServicesHowtoactuallyusethem_11C9F/image.png)

After you click Go it shows you the various services available and operations for each service. The Search Service is the one we will want.

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/ILM2WebServicesHowtoactuallyusethem_11C9F/image_thumb_3.png)](http://www.ilmbestpractices.com/blog/uploaded_images/ILM2WebServicesHowtoactuallyusethem_11C9F/image_3.png)

Once you click OK you see the following show up under service reference:

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/ILM2WebServicesHowtoactuallyusethem_11C9F/image_thumb_4.png)](http://www.ilmbestpractices.com/blog/uploaded_images/ILM2WebServicesHowtoactuallyusethem_11C9F/image_4.png)

An enumeration.wsdl file is generated and your app.config file will also be populated with lots of settings such as this one.

```
   <binding name\="ServiceMultipleTokenBinding\_Search" closeTimeout\="00:01:00"  
                    openTimeout\="00:01:00" receiveTimeout\="00:10:00" sendTimeout\="00:01:00"  
                    bypassProxyOnLocal\="false" transactionFlow\="false" hostNameComparisonMode\="StrongWildcard"  
                    maxBufferPoolSize\="524288" maxReceivedMessageSize\="65536"  
                    messageEncoding\="Text" textEncoding\="utf-8" useDefaultWebProxy\="true"  
                    allowCookies\="false" contextProtectionLevel\="Sign"\>  
                    <readerQuotas maxDepth\="32" maxStringContentLength\="8192" maxArrayLength\="16384"  
                        maxBytesPerRead\="4096" maxNameTableCharCount\="16384" />  
                    <reliableSession ordered\="true" inactivityTimeout\="00:10:00"  
                        enabled\="false" />  
                    <security mode\="Message"\>  
                        <transport clientCredentialType\="Windows" proxyCredentialType\="None"  
                            realm\="" />  
                        <message clientCredentialType\="Windows" negotiateServiceCredential\="true"  
                            algorithmSuite\="Default" establishSecurityContext\="false" />  
                    </security\>
```  
<br />.csharpcode, .csharpcode pre<br />{<br /> font-size: small;<br /> color: black;<br /> font-family: consolas, "Courier New", courier, monospace;<br /> background-color: #ffffff;<br /> /\*white-space: pre;\*/<br />}<br />.csharpcode pre { margin: 0em; }<br />.csharpcode .rem { color: #008000; }<br />.csharpcode .kwrd { color: #0000ff; }<br />.csharpcode .str { color: #006080; }<br />.csharpcode .op { color: #0000c0; }<br />.csharpcode .preproc { color: #cc6633; }<br />.csharpcode .asp { background-color: #ffff00; }<br />.csharpcode .html { color: #800000; }<br />.csharpcode .attr { color: #ff0000; }<br />.csharpcode .alt <br />{<br /> background-color: #f4f4f4;<br /> width: 100%;<br /> margin: 0em;<br />}<br />.csharpcode .lnum { color: #606060; }  
  

You can also generate this info through a command line approach using the svcutil.exe utility.

  
  

Then in your code you make use of it like this as you see in my code:

  
  

>   
> ```
> Dim scReporting As ILM\_RMS.SearchClient   
> scReporting = New ILM\_RMS.SearchClient("ServiceMultipleTokenBinding\_Search")
> ```  
> <br />.csharpcode, .csharpcode pre<br />{<br /> font-size: small;<br /> color: black;<br /> font-family: consolas, "Courier New", courier, monospace;<br /> background-color: #ffffff;<br /> /\*white-space: pre;\*/<br />}<br />.csharpcode pre { margin: 0em; }<br />.csharpcode .rem { color: #008000; }<br />.csharpcode .kwrd { color: #0000ff; }<br />.csharpcode .str { color: #006080; }<br />.csharpcode .op { color: #0000c0; }<br />.csharpcode .preproc { color: #cc6633; }<br />.csharpcode .asp { background-color: #ffff00; }<br />.csharpcode .html { color: #800000; }<br />.csharpcode .attr { color: #ff0000; }<br />.csharpcode .alt <br />{<br /> background-color: #f4f4f4;<br /> width: 100%;<br /> margin: 0em;<br />}<br />.csharpcode .lnum { color: #606060; }

  
  

See how to use the Namespace that you setup when you made the service reference, and how you need  use the binding name setup in the app.config file. Instead of using the settings in the config file you can use a programmatic approach to setting up the bindings. Look at the example from Mark Struck's C# code:

  
  

>   
> ```
> WSHttpContextBinding wsBinding = new WSHttpContextBinding();   
> // Cannot use WSHttpBinding since it does not allow you to Sign the EnumerationContext element   
> // WsHttpContextBinding provides a property called ContextProtectionLevel which defaults to Sign, which is   
> // what is needed to communicate with the web service when the action is Pull.   
> // WsHttpBinding will work if you are just calling the web service with the Enumerate action.   
> //WSHttpBinding wsBinding = new WSHttpBinding();   
>   
> // Set binding properties   
> wsBinding.ReceiveTimeout = new TimeSpan( 0, 5, 0);   
> wsBinding.SendTimeout = new TimeSpan( 0, 5, 0);   
> wsBinding.Security.Mode = SecurityMode.Message;   
> wsBinding.Security.Message.EstablishSecurityContext = false;   
> wsBinding.Security.Message.NegotiateServiceCredential = true;   
> wsBinding.Security.Message.ClientCredentialType = MessageCredentialType.Windows;   
> wsBinding.Security.Message.AlgorithmSuite = System.ServiceModel.Security.SecurityAlgorithmSuite.Default;   
>   
> // Create EndpointAddress object and create the SearchClient object with the binding and endpointaddress objects   
> EndpointAddress ep = new EndpointAddress(ILMSERVICE\_URI\_ENUMERATION);   
> SearchClient searchClient = new SearchClient(wsBinding, ep);
> ```

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices