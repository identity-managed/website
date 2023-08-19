---
title: 'CSExport -- Getting the ILM Connector Space into SQL'
date: 2008-11-11T14:30:00.001-07:00
draft: false
url: /2008/11/csexport-getting-ilm-connector-space.html
---

How can I query the ILM Connector Space?

"You can't." -- Yes you can.

"You have to WMI." --  But WMI is limited in what you can query and slow

"You have to use CSExport and then use XML tools." -- that works, but this may be better

The above are various answers you may receive. However, thanks to the power of SQLXML we can issue SQL queries against the ILM Connector Space (after it has been exported using CSExport).

The following code will only work on SQL 2005. Some of the [SQLXML tricks involved here have been described previously](http://www.ilmbestpractices.com/blog/2008/07/pending-exports-report-in-ilm.html)

So I will discuss some of the new tricks.

The csexport file spits out XML that looks a lot like entity attribute value schema and this means that each attribute gets its own row when you bring it into SQL. Since that doesn't work well for me to write further queries I use a pivot operator to make the data relational.

The code below will retrieve data from the pending import holograms of an AD connectorspace and doesn't handle multi-valued attributes.

```
SET NOCOUNT ON
```  
  
```
DECLARE @ADXML TABLE (ADID int identity (1,1), XMLFROMCS XML)
```  
  
```
INSERT @ADXML (XMLFROMCS)
```  
  
```
SELECT \* 
```  
  
```
FROM OPENROWSET(BULK 'C:\\FuzzyLogic\\ADExport\\ADExport.xml',SINGLE\_BLOB) AS AD
```  
  

  
  
```
DECLARE @ADXMLData XML
```  
  

  
  
```
SELECT @ADXMLData = XMLFROMCS
```  
  
```
FROM @ADXML
```  
  

  
  
```
DECLARE @docHandle int
```  
  
```
EXEC sp\_xml\_preparedocument @docHandle OUTPUT, @ADXMLData
```  
  

  
  
```
TRUNCATE TABLE dbo.adUsers 
```  
  

  
  
```
INSERT dbo.adUsers (dn, \[cn\],\[department\],\[displayname\],\[employeeid\],\[givenname\],\[mail\],\[sn\],\[title\])
```  
  

  
  
```
SELECT dn, \[cn\],\[department\],\[displayname\],\[employeeid\],\[givenname\],\[mail\],\[sn\],\[title\]
```  
  
```
FROM
```  
  
```
    (
```  
  
```
            SELECT dn, attrname, attrvalue  
```  
  
```
            FROM OPENXML(@docHandle, N'/cs-objects/cs-object/pending-import-hologram/entry/attr/value',2)  
```  
  
```
             WITH 
```  
  
```
                (dn nvarchar(450) '../../@dn'
```  
  
```
                ,primaryobjectclass nvarchar(450) '../../primary-objectclass'
```  
  
```
                ,attrname nvarchar(450) '../@name'
```  
  
```
                ,attrvalue nvarchar(450) '.'
```  
  
```
                ,multivalued nvarchar(450) '../@multivalued'
```  
  
```
                ) adusers
```  
  
```
            WHERE adusers.primaryobjectclass = 'user' AND adusers.multivalued = 'false'
```  
  
```
                AND attrname in ('cn','department','displayname', 'employeeid', 'givenName', 'mail', 'sn','title') 
```  
  
```
        ) AS ADList1
```  
  

  
  
```
    PIVOT (MIN(attrvalue) FOR attrname in (\[cn\],\[department\],\[displayname\],\[employeeid\],\[givenname\],\[mail\],\[sn\],\[title\])
```  
  
```
 )AS ADUserPivot
```  
  

  
  
```
EXEC sp\_xml\_removedocument @docHandle 
```  

  
<br />.csharpcode, .csharpcode pre<br />{<br /> font-size: small;<br /> color: black;<br /> font-family: consolas, "Courier New", courier, monospace;<br /> background-color: #ffffff;<br /> /\*white-space: pre;\*/<br />}<br />.csharpcode pre { margin: 0em; }<br />.csharpcode .rem { color: #008000; }<br />.csharpcode .kwrd { color: #0000ff; }<br />.csharpcode .str { color: #006080; }<br />.csharpcode .op { color: #0000c0; }<br />.csharpcode .preproc { color: #cc6633; }<br />.csharpcode .asp { background-color: #ffff00; }<br />.csharpcode .html { color: #800000; }<br />.csharpcode .attr { color: #ff0000; }<br />.csharpcode .alt <br />{<br /> background-color: #f4f4f4;<br /> width: 100%;<br /> margin: 0em;<br />}<br />.csharpcode .lnum { color: #606060; }

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices