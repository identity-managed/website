---
title: 'Pending Exports Report in ILM'
date: 2008-07-30T14:52:00.001-07:00
draft: false
url: /2008/07/pending-exports-report-in-ilm.html
tags: 
- ILM
- ILM 2 Beta 3
- XML
- SQL Server
---

Hopefully this topic will stir up some excitement among those wondering how to query objects in the connector space. The technique I am about to explicate for you works for both exports and imports.

As many of you aware, my colleague and fellow ILM MVP Brad Turner created the community reporting pack for MIIS/ILM some time ago. This is a package of reports written in SQL Server Reporting Services (SSRS).

Most of you are also aware that you can tell an import or export run profile step to drop an audit file. The audit file is in DSML format (an XML format). You can use XML files as the source for SSRS reports, they can also be used.

A later report he created was for Pending Exports, to show clients what records are about to be exported (drop audit file and stop) or what records were just exported (drop audit file).

1) Turn on the drop audit file for the export run profile step.

2) Create a virtual directory in IIS that points to the MAData subfolder location and allows you to see the file

3) Create a data source in SSRS for that file and only that file. This means you have to create a data source for each audit file. Wow -- doable but painful!

A short while ago I took this process and made it even slicker. I present the background of all this to show why Brad and I form the nucleus of a great team. I had not thought of creating a report based on the audit file. I viewed the audit file as a troubleshooting technique, not as a great way to be able to report on exports or imports. My inspiration was how to make this more flexible.

I created a stored procedure (only works on SQL 2005) that uses SQLXML (specifically the sp\_xml\_preparedocument and OpenXML to shred the XML data to relational data). 

Additionally, I created the stored procedure so that it can accept a lot of parameters, allowing us to report the pending exports (or just exported) for any of the MAs).

That means that we only need one data source -- pointing to the database that houses the stored procedure.

First allow me to demonstrate the basic technique:

SET NOCOUNT ON

DECLARE @ADXMLData XML

SELECT @ADXMLData = BulkColumn   
FROM OPENROWSET(BULK 'C:\\Ensynch\_projects\\Reports\\ILMReports\\copy of admaexports.xml',SINGLE\_NCLOB) AS AD

DECLARE @docHandle int  
EXEC sp\_xml\_preparedocument @docHandle OUTPUT, @ADXMLData, '<mmsml xmlns:a="[http://www.microsoft.com/mms/mmsml/v2"/](http://www.microsoft.com/mms/mmsml/v2)\>'

            SELECT \*   
            FROM OPENXML(@docHandle, N'//a:mmsml/a:directory-entries/a:delta/a:dn-attr/a:dn-value/a:dn',2)   
             With (  
                    DeltaOp varchar(100) '../../../@operation'  
                    ,DNAOp varchar(100) '../../@operation'  
                    ,DNVOp varchar(100) '../@operation'  
                    --,ObjType varchar(50) '../../../primary-objectclass'  
                    ,ObjectDN varchar(1000) '../../../@dn'  
                    ,AttrName varchar(100) '../../@name'  
                    ,dn        varchar(1000) '.'  
            ) Export  
ORDER BY GroupDN

EXEC sp\_xml\_removedocument @docHandle

For this query I was first focused on some group updates. I need to show the client how we were going to update their distribution lists.

This query takes the XML from the DSML file and shreds it back to relational data like so

update

add

 

CN=Group1, OU=Distribution Groups, OU=Enterprise Groups, DC=Aclient,DC=org

member

CN=MontyHALL, OU=Groupwise Directory Sync - SJHS,OU=Exchange, DC=Aclient,DC=org

update

add

 

CN=Group1, OU=Distribution Groups, OU=Enterprise Groups, DC=Aclient,DC=org

member

CN=Joe Montana, OU=Groupwise Directory Sync - SJHS,OU=Exchange, DC=Aclient,DC=org

update

add

 

CN=Group1, OU=Distribution Groups, OU=Enterprise Groups, DC=Aclient,DC=org

member

CN=Steve Young, OU=Groupwise Directory Sync - SJHS,OU=Exchange, DC=Aclient,DC=org

update

add

 

CN=Group1, OU=Distribution Groups, OU=Enterprise Groups, DC=Aclient,DC=org

member

CN=Fred Idaho, OU=Groupwise Directory Sync - SJHS,OU=Exchange, DC=Aclient,DC=org

update

add

add

CN=Group2, OU=Distribution Groups, OU=Enterprise Groups, DC=Aclient,DC=org

member

CN=Fred Idaho, OU=Groupwise Directory Sync - SJHS,OU=Exchange, DC=Aclient,DC=org

update

add

add

CN=Group2, OU=Distribution Groups, OU=Enterprise Groups, DC=Aclient,DC=org

member

CN=MontyHALL, OU=Groupwise Directory Sync - SJHS,OU=Exchange, DC=Aclient,DC=org

update

add

add

CN=Group2, OU=Distribution Groups, OU=Enterprise Groups, DC=Aclient,DC=org

member

CN=Joe Montana, OU=Groupwise Directory Sync - SJHS,OU=Exchange, DC=Aclient,DC=org

Next week I will show how to add the parameters and then I will show how to make the report. If you are lucky I might even make a video and post it!

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices