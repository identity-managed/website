---
title: 'Installing a Multi-Instance SQL 2005 Cluster'
date: 2008-10-15T00:54:00.001-07:00
draft: false
url: /2008/10/installing-multi-instance-sql-2005.html
tags: 
- SQL Clustering
- SQL Server
---

#### Hi, I'm installing SQL Server 2005 in 2 node ...
[Unknown](https://www.blogger.com/profile/05001115668295519336 "noreply@blogger.com") - <time datetime="2010-06-23T17:36:35.794-07:00">Jun 3, 2010</time>

Hi,  
  
I'm installing SQL Server 2005 in 2 node cluster setup and I'm getting the below error:  
  
TITLE: Microsoft SQL Server 2005 Setup  
\------------------------------  
  
SQL Server Setup has determined that the following account properties are not specified: 'SQLBROWSERACCOUNT' . The properties specify the startup account for the services that are installed. To proceed, refer to the template.ini and set the properties to valid account names. If you are specifying a windows user account, you must also specify the password for the account.  
  
For help, click: http://go.microsoft.com/fwlink?LinkID=20476&ProdName=Microsoft+SQL+Server&ProdVer=9.00.1399.06&EvtSrc=setup.rll&EvtID=28006&EvtType=sqlca%5csqlguica.cpp%40SetUnattendedSvcAccountProp%40SetUnattendedSvcAccountProp%40x6d66  
  
\------------------------------  
BUTTONS:  
  
OK  
  
  
On node1, before installing SQL Server 2005 on this 2 node cluster setup, I have installed a stand alone SQL Server 2008 instance & installed SQL Server 2005 backward compatibility components to run a DTS package  
  
Please advice that where can I specify the properties for 'SQLBROWSERACCOUNT' to resolve the issue  
  
You said that this issue will occur when installing 2nd or 3rd instances. But for me this is a 1st failover cluster instance where its giving the same error.
<hr />
