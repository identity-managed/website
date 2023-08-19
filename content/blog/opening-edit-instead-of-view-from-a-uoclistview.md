---
title: 'Opening Edit instead of view from a uocListView'
date: 2012-04-27T06:57:00.001-07:00
draft: false
url: /2012/04/opening-edit-instead-of-view-from.html
tags: 
- RCDC
- Forefront Identity Manager
- FIM
---

When using the uocListView control in the FIM RCDC you can have it return a list of objects. However when you open them, they also open for viewing, not editing.

The key to this is to add a button control inside the uocListView control. You then specify the redirectURL property for the button. Additionally ShowActionBar must be true, ItemClickBehavior must be ModelessDialog (which is the default). Enable Selection must also be true.

I examined the Policy Explorer to figure this out.

Here is an example that [I first posted on the forum](http://social.technet.microsoft.com/Forums/en-US/ilm2/thread/6c693af5-0f89-43bd-b84e-623fb47f33df):

<my:Control my:Name="RequestViewCompleted" my:TypeName="UocListView" my:Caption="All Completed Role Requests" my:ExpandArea="true" my:RightsLevel="{Binding Source=rights, Path=Owner}">

<my:Buttons>

<my:Button my:Name="Edit" my:Caption="Edit" my:ImageUrl="/\_layouts/images/MSILM2/details.png" my:ClickBehavior="ModalDialog" my:EnableMode="OnlyOne" my:RedirectUrl="../customized/EditCustomizedObject.aspx" />

</my:Buttons>

<my:Properties> <my:Property my:Name="EmptyResultText" my:Value="There are no role requests for this role." />

<my:Property my:Name="PageSize" my:Value="5" />

<my:Property my:Name="SearchControlAutoPostback" my:Value="true" />

<my:Property my:Name="SearchOnLoad" my:Value="true" />

<my:Property my:Name="ShowTitleBar" my:Value="true" /> <my:Property my:Name="ShowActionBar" my:Value="true" />

<my:Property my:Name="ShowPreview" my:Value="false" />

<my:Property my:Name="ShowSearchControl" my:Value="true" />

<my:Property my:Name="EnableSelection" my:Value="true" />

<my:Property my:Name="SingleSelection" my:Value="true" />

<my:Property my:Name="ItemClickBehavior" my:Value="ModelessDialog" />

<my:Property my:Name="UsageKeywords" my:Value="RoleRequestCompleted"/>

</my:Properties>

</my:Control>

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices