---
title: 'Calling a stored procedure in an ADFS claims rule'
date: 2011-09-01T06:34:00.001-07:00
draft: false
url: /2011/09/calling-stored-procedure-in-adfs-claims.html
tags: 
- SQL
- ADFS
- Federation
---

After you have setup your [SQL Attribute Claims Store in ADFS](http://blog.ilmbestpractices.com/2011/09/troubleshooting-sql-attribute-stores.html). If you want to use it and in fact test it you must set up a claims rule that makes use of it. To do this you must create a claim using a custom rule, which allows you to employ the [claims rule language](http://technet.microsoft.com/en-us/library/adfs2-help-the-claim-rule-language(WS.10).aspx).

The following [technet entry is a good start](http://technet.microsoft.com/en-us/library/adfs2-help-attribute-stores(WS.10).aspx) as it illustrates how to enter a SQL Query and even a stored procedure.

SQL Query:

c:\[Type == "[http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress](http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress)"\]

\=> issue(store = "SQLClaims", types = ("[http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress](http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress)"), query = "SELECT myID from employees where @myp={0}", param = c.Value);

Stored Procedure:

c:\[Type == "[http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress](http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress)"\]

\=> issue(store = "SQLClaims", types = ("[http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress](http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress)"), query = "EXEC dbo.test @myp={0}", param = c.Value);

[![image](http://www.ilmbestpractices.com/blog/uploaded_images/Calling-a-stored-procedure-in-an-ADFS-cl_59B4/image_thumb.png "image")](http://www.ilmbestpractices.com/blog/uploaded_images/Calling-a-stored-procedure-in-an-ADFS-cl_59B4/image.png)

Note that the parameter{0} is not surrounded by single quotes.

One may ask what gets passed in as the parameter? The incoming claim value of course. In this case the emailaddress as defined in the c:\[Type == "[http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress](http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress)"\]

One might also ask what happens if I make a query or stored procedure that returns more than one value? Your claims transformation rule adds all the resulting values to the token as claims of the same type.

One might also ask what happens if my query or stored procedure returns more than one column? An error results and the whole process fails.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices