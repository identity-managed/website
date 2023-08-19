---
title: 'ILM 2 RC 0 -- Luke, Check the Transaction Log!'
date: 2009-08-14T21:16:00.001-07:00
draft: false
url: /2009/08/ilm-2-rc-0-luke-check-transaction-log.html
---

A few weeks ago I encountered an ASP.NET error when I tried to access [http://myilmserver/identitymanagement/](http://myilmserver/identitymanagement/)

Eventually I went to my SQL Server and discovered that despite having space on the disk and Autogrow turned on the Transaction Log was full and wouldn't grow anymore.

So if you encounter this error then maybe you too can listen to the force telling you to check the SQL Server Transaction Log for MSILM.

In the event log I saw this:

Log Name:      Application  
Source:        ASP.NET 2.0.50727.0  
Event ID:      1309  
Task Category: Web Event  
Level:         Warning  
Keywords:      Classic  
User:          N/A  
Computer:     myILMServer  
Description:  
Event code: 3005  
Event message: An unhandled exception has occurred.  
Event sequence: 4  
Event occurrence: 1  
Event detail code: 0

Application information:   
      
    Trust level: WSS\_Minimal  
    Application Virtual Path: /  
    Application Path: C:\\inetpub\\wwwroot\\wss\\VirtualDirectories\\80\\  
    Machine name: PHX-52N-ILMWF91  
Process information:  
    Process ID: 2256  
    Process name: w3wp.exe  
    Account name: ILMTEST\\svc.wss  
Exception information:  
    Exception type: SerializationException  
    Exception message: Error in line 1 position 350. Expecting element 'Metadata' from namespace 'http://schemas.xmlsoap.org/ws/2004/09/mex'.. Encountered 'Element'  with name 'Fault', namespace 'http://www.w3.org/2003/05/soap-envelope'.   
Request information:  
    Request URL: [http://myilmserver/identitymanagement/default.aspx](http://myilmserver/identitymanagement/default.aspx)  
    Request path: /identitymanagement/default.aspx  
    User host address: 10.12.13.14  
    User: ILM\\Administrator  
    Is authenticated: True  
    Authentication Type: Negotiate  
    Thread account name: ILM\\svc.wss  
Thread information:  
    Thread ID: 4  
    Thread account name: ILMT\\svc.wss  
    Is impersonating: False  
    Stack trace:    at System.Runtime.Serialization.DataContractSerializer.InternalReadObject(XmlReaderDelegator xmlReader, Boolean verifyObjectName)  
   at System.Runtime.Serialization.XmlObjectSerializer.ReadObjectHandleExceptions(XmlReaderDelegator reader, Boolean verifyObjectName)  
   at System.ServiceModel.Channels.Message.GetBody\[T\](XmlObjectSerializer serializer)  
   at System.ServiceModel.Channels.Message.GetBody\[T\]()  
   at Microsoft.ResourceManagement.WebServices.MetadataClient.Get(String dialect, String identifier)  
   at Microsoft.ResourceManagement.WebServices.Client.ResourceManagementClient.SchemaManagerImplementation.RefreshSchema()  
   at Microsoft.ResourceManagement.WebServices.ResourceManager.get\_SchemaManager()  
   at Microsoft.ResourceManagement.WebServices.ResourceManager..ctor(String typeName, LocaleAwareClientHelper localePreferences, ContextualSecurityToken securityToken)  
   at Microsoft.IdentityManagement.WebUI.Controls.ConfigurationModelBase.RetrieveResources(String type, List\`1 attributes)  
   at Microsoft.IdentityManagement.WebUI.Controls.PortalUIConfigurationModel.RetrievePortalUIConfiguration()  
   at Microsoft.IdentityManagement.WebUI.Controls.PortalUIConfigurationModel.get\_PortalUI()  
   at Microsoft.IdentityManagement.WebUI.Controls.PortalUIConfigurationModel.get\_BrandingLeftImageUrl()  
   at Microsoft.IdentityManagement.WebUI.Controls.BrandBar.get\_BrandTable()  
   at Microsoft.IdentityManagement.WebUI.Controls.BrandBar.CreateChildControls()  
   at System.Web.UI.Control.EnsureChildControls()  
   at System.Web.UI.Control.PreRenderRecursiveInternal()  
   at System.Web.UI.Control.PreRenderRecursiveInternal()  
   at System.Web.UI.Control.PreRenderRecursiveInternal()  
   at System.Web.UI.Control.PreRenderRecursiveInternal()  
   at System.Web.UI.Control.PreRenderRecursiveInternal()  
   at System.Web.UI.Page.ProcessRequestMain(Boolean includeStagesBeforeAsyncPoint, Boolean includeStagesAfterAsyncPoint)

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices