---
title: 'Troubleshooting SQL Attribute Stores with ADFS'
date: 2011-09-01T06:21:00.001-07:00
draft: false
url: /2011/09/troubleshooting-sql-attribute-stores.html
tags: 
- SQL
- ADFS
---

Several [others have showed how to define SQL attribute stores with ADFS](http://www.spmcm.me/Blog/Lists/Posts/Post.aspx?ID=8).

Note that when entering the connection string there is no validation or feedback to the administrator. If there is a problem you usually won’t see it until you setup a claims rule that uses it and you get an error. So make certain to carefully build and test your [connection string](http://connectionstrings.com/). Remember that if you use integrated authentication to connect to the SQL Server that it will run under the context of your ADFS Service account so you will need to grant your ADFS service account permissions to the SQL Server and Database.

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/SQL-Attribute-Stores-with-ADFS_6578/image_thumb.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/SQL-Attribute-Stores-with-ADFS_6578/image.png)

Troubleshooting

For example you might get event 149

During processing of the Federation Service configuration, the attribute store 'SQLClaims' could not be loaded.   
Attribute store type: Microsoft.IdentityServer.ClaimsPolicy.Engine.AttributeStore.Sql.SqlAttributeStore, Microsoft.IdentityServer.ClaimsPolicy

User Action  
If you are using a custom attribute store, verify that the custom attribute store is configured using AD FS 2.0 Management snap-in.

Additional Data  
POLICY3906: Could not parse the parameter as a valid connection string.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices