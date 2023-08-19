---
title: 'Object reference not set to an instance of an object'
date: 2010-06-13T12:00:00.001-07:00
draft: false
url: /2010/06/object-reference-not-set-to-instance-of.html
tags: 
- Forefront Identity Manager
- Identity Management
- FIM
---

Lessons learned:

1) Run the [Do a FIM MA account configuration quick test](http://social.technet.microsoft.com/Forums/en-US/ilm2/thread/215ae0cf-e406-4a76-8596-057c7e184626) script.

2) Always refresh the schema of the FIM MA using the real FIM MA Service Account which we usually call svc-FIMMA.

Scenario:

You have just modified the schema of FIM Service by creating a new Boolean attribute and have bound it to the user resource type. You refresh the FIM Schema, select the new attribute setup a direct export attribute flow from the corresponding Boolean metaverse attribute to the FIM MA attribute. You sync and the only pending export is to this attribute, and then when you run the export to FIM MA you get:

failed-modification-via-web-services

Then when you click on details:

> There is an error executing a web service object modification request.  
> Type: System.NullReferenceException
> 
> Message: Object reference not set to an instance of an object.
> 
> Stack Trace:    at MIIS.ManagementAgent.RavenMA.DoAttributeLevelExport(DataSourceObject dsObject, String objClass, UninitializedResource resource)  
>    at MIIS.ManagementAgent.RavenMA.ExportObjectModification(DataSourceObject dsObject, SchemaManager schemaManager)  
>    at MIIS.ManagementAgent.RavenMA.Export(DataSourceObject dsObject)
> 
> Inner Exception:

I have encountered this twice and [Brad once](http://social.technet.microsoft.com/Forums/en-US/ilm2/thread/ace5af61-bc44-4187-9190-4d1a693814ce). The first time (1 month ago)  I discovered that the FIM MA was set to use the svc-fimws (this is the credentials used to run the FIM Service) user account instead of the svc-fimma (the account that actually belongs to the Synchronization Engine Set and therefore has all of the permissions to modify objects in the portal and bypasses the authn and authz workflows and is sometimes referred to as the Built-in Synchronization account). So I changed the FIM MA to use the svc-fimma account and when prompted clicked yes Refresh Schema.  The [Do a FIM MA account configuration quick test](http://social.technet.microsoft.com/Forums/en-US/ilm2/thread/215ae0cf-e406-4a76-8596-057c7e184626) script had told me that the two weren’t the same (go [FIM Scriptbox](http://social.technet.microsoft.com/Forums/en-US/ilm2/thread/807617bc-b560-4cbe-a137-b9f338bfbd8e)!)

Which means that when I ran the refresh schema the first time it was under the svc-fimws account not the svc-fimma account.

The second time we refreshed the schema using the credentials of an admin user as opposed to the svc-fimma credentials. I tried refreshing the schema with the svc-fimma account but of course it said no changes. I tried stopping and starting all of the services. I turned on messaging logging (this isn’t even sending messages it is dying on the MA without even talking to the web service). So after carefully studying my memory (foolish me I didn’t blog it or make a note) and the request history on the other system I remembered what the root problem and solution had been. But I had already checked if the MA was using the true Built-in Synchronization Account using the [Do a FIM MA account configuration quick test](http://social.technet.microsoft.com/Forums/en-US/ilm2/thread/215ae0cf-e406-4a76-8596-057c7e184626) script . So then I thought what if I create the _exact same_ problem I had last time and then fix it. So I changed the FIM MA to use an admin user account and when prompted clicked yes Refresh Schema. Then I changed the FIM MA to use the svc-fimma account and when prompted clicked yes Refresh Schema. Then my export worked!

Lessons learned:

1) Run the [Do a FIM MA account configuration quick test](http://social.technet.microsoft.com/Forums/en-US/ilm2/thread/215ae0cf-e406-4a76-8596-057c7e184626) script.

2) Always refresh the schema of the FIM MA using the real FIM MA Service Account which we usually call svc-FIMMA. (Anyone from Microsoft want to give an official statement of best practice on that?)

I plan to repro this in a test environment to ensure this is the problem.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices