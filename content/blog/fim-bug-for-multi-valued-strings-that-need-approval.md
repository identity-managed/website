---
title: 'FIM Bug for multi-valued strings that need approval'
date: 2011-06-28T09:52:00.001-07:00
draft: false
url: /2011/06/fim-bug-for-multi-valued-strings-that.html
tags: 
- Forefront Identity Manager
- FIM
---

I think I found a bug in FIM Version 4.0.3576.2 take a look:

It appears that when you have a multi-valued string attribute when you add more than 1 value at a time and you need approval to create the object or to update the attribute, the request will fail. In the event log you will see an error (UnwillingToPerformException … CREATE UNIQUE INDEX statement terminated because a duplicate key was found for the object).

[![clip_image001](http://www.ilmbestpractices.com/blog/uploaded_images/05e56e3f80a8_89E5/clip_image001_thumb.png "clip_image001")](http://www.ilmbestpractices.com/blog/uploaded_images/05e56e3f80a8_89E5/clip_image001.png)

[![clip_image002](http://www.ilmbestpractices.com/blog/uploaded_images/05e56e3f80a8_89E5/clip_image002_thumb.png "clip_image002")](http://www.ilmbestpractices.com/blog/uploaded_images/05e56e3f80a8_89E5/clip_image002.png)

[![clip_image003](http://www.ilmbestpractices.com/blog/uploaded_images/05e56e3f80a8_89E5/clip_image003_thumb.png "clip_image003")](http://www.ilmbestpractices.com/blog/uploaded_images/05e56e3f80a8_89E5/clip_image003.png)

Log Name: Forefront Identity Manager

Source: Microsoft.ResourceManagement

Date: 6/27/2011 6:33:52 PM

Event ID: 3

Task Category: None

Level: Error

Keywords: Classic

User: N/A

Computer: fimserver

Description:

Microsoft.ResourceManagement.WebServices.Exceptions.UnwillingToPerformException: Other ---> System.Data.SqlClient.SqlException: Reraised Error 50000, Level 16, State 1, Procedure ReRaiseException, Line 37, Message: Reraised Error 50000, Level 16, State 1, Procedure ReRaiseException, Line 37, Message: Reraised Error 1505, Level 16, State 1, Procedure ReEvaluateRequestOutputString, Line 53, Message: The CREATE UNIQUE INDEX statement terminated because a duplicate key was found for the object name 'dbo.#reevaluateRequestOutputStringRemovalCandidate\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_0000000175F1' and the index name 'IX\_ReEvaluateRequestRequestOutputStringRemovalCandidate\_ObjectKey\_ObjectTypeKey\_AttributeKey\_ValueString'. The duplicate key value is (23564, 32698, 32655, 0).

Uncommittable transaction is detected at the end of the batch. The transaction is rolled back.

at System.Data.SqlClient.SqlConnection.OnError(SqlException exception, Boolean breakConnection)

at System.Data.SqlClient.TdsParser.ThrowExceptionAndWarning(TdsParserStateObject stateObj)

at System.Data.SqlClient.TdsParser.Run(RunBehavior runBehavior, SqlCommand cmdHandler, SqlDataReader dataStream, BulkCopySimpleResultSet bulkCopyHandler, TdsParserStateObject stateObj)

at System.Data.SqlClient.SqlDataReader.ConsumeMetaData()

at System.Data.SqlClient.SqlDataReader.get\_MetaData()

at System.Data.SqlClient.SqlCommand.FinishExecuteReader(SqlDataReader ds, RunBehavior runBehavior, String resetOptionsString)

at System.Data.SqlClient.SqlCommand.RunExecuteReaderTds(CommandBehavior cmdBehavior, RunBehavior runBehavior, Boolean returnStream, Boolean async)

at System.Data.SqlClient.SqlCommand.RunExecuteReader(CommandBehavior cmdBehavior, RunBehavior runBehavior, Boolean returnStream, String method, DbAsyncResult result)

at System.Data.SqlClient.SqlCommand.RunExecuteReader(CommandBehavior cmdBehavior, RunBehavior runBehavior, Boolean returnStream, String method)

at System.Data.SqlClient.SqlCommand.ExecuteReader(CommandBehavior behavior, String method)

at System.Data.SqlClient.SqlCommand.ExecuteReader()

at Microsoft.ResourceManagement.Data.DataAccess.ProcessRequest(RequestType request)

\--- End of inner exception stack trace ---

Event Xml:

<Event xmlns="http://schemas.microsoft.com/win/2004/08/events/event">

<System>

<Provider Name="Microsoft.ResourceManagement" />

<EventID Qualifiers="0">3</EventID>

<Level>2</Level>

<Task>0</Task>

<Keywords>0x80000000000000</Keywords>

<TimeCreated SystemTime="2011-06-28T01:33:52.000000000Z" />

<EventRecordID>9448</EventRecordID>

<Channel>Forefront Identity Manager</Channel>

<Computer>fimserver</Computer>

<Security />

</System>

<EventData>

<Data>Microsoft.ResourceManagement.WebServices.Exceptions.UnwillingToPerformException: Other ---&gt; System.Data.SqlClient.SqlException: Reraised Error 50000, Level 16, State 1, Procedure ReRaiseException, Line 37, Message: Reraised Error 50000, Level 16, State 1, Procedure ReRaiseException, Line 37, Message: Reraised Error 1505, Level 16, State 1, Procedure ReEvaluateRequestOutputString, Line 53, Message: The CREATE UNIQUE INDEX statement terminated because a duplicate key was found for the object name 'dbo.#reevaluateRequestOutputStringRemovalCandidate\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_0000000175F1' and the index name 'IX\_ReEvaluateRequestRequestOutputStringRemovalCandidate\_ObjectKey\_ObjectTypeKey\_AttributeKey\_ValueString'. The duplicate key value is (23564, 32698, 32655, 0).

Uncommittable transaction is detected at the end of the batch. The transaction is rolled back.

at System.Data.SqlClient.SqlConnection.OnError(SqlException exception, Boolean breakConnection)

at System.Data.SqlClient.TdsParser.ThrowExceptionAndWarning(TdsParserStateObject stateObj)

at System.Data.SqlClient.TdsParser.Run(RunBehavior runBehavior, SqlCommand cmdHandler, SqlDataReader dataStream, BulkCopySimpleResultSet bulkCopyHandler, TdsParserStateObject stateObj)

at System.Data.SqlClient.SqlDataReader.ConsumeMetaData()

at System.Data.SqlClient.SqlDataReader.get\_MetaData()

at System.Data.SqlClient.SqlCommand.FinishExecuteReader(SqlDataReader ds, RunBehavior runBehavior, String resetOptionsString)

at System.Data.SqlClient.SqlCommand.RunExecuteReaderTds(CommandBehavior cmdBehavior, RunBehavior runBehavior, Boolean returnStream, Boolean async)

at System.Data.SqlClient.SqlCommand.RunExecuteReader(CommandBehavior cmdBehavior, RunBehavior runBehavior, Boolean returnStream, String method, DbAsyncResult result)

at System.Data.SqlClient.SqlCommand.RunExecuteReader(CommandBehavior cmdBehavior, RunBehavior runBehavior, Boolean returnStream, String method)

at System.Data.SqlClient.SqlCommand.ExecuteReader(CommandBehavior behavior, String method)

at System.Data.SqlClient.SqlCommand.ExecuteReader()

at Microsoft.ResourceManagement.Data.DataAccess.ProcessRequest(RequestType request)

\--- End of inner exception stack trace ---</Data>

</EventData>

</Event>

[![clip_image004](http://www.ilmbestpractices.com/blog/uploaded_images/05e56e3f80a8_89E5/clip_image004_thumb.png "clip_image004")](http://www.ilmbestpractices.com/blog/uploaded_images/05e56e3f80a8_89E5/clip_image004.png)

So I looked up the stored procedure mentioned in the Error Message.

We can see that this stored procedure can get called from a lot of places and so can be an issue in many spots.

The problem is found in the text of the ReEvaluateRequestOutputString stored procedure excerpted here below with my comments added inside /\* \*/:

SELECT DISTINCT

\[requestOriginal\].\[ObjectKey\] AS N'ObjectKey',

\[requestOriginal\].\[ObjectTypeKey\] AS N'ObjectTypeKey',

\[requestOriginal\].\[AttributeKey\] AS N'AttributeKey',

\[requestOriginal\].\[ValueString\] AS N'ValueString',

\[requestOriginal\].\[Deleted\] AS N'Deleted'

INTO #reevaluateRequestOutputStringRemovalCandidate

FROM \[fim\].\[RequestOutputString\] AS \[requestOriginal\]

WHERE

\[requestOriginal\].\[RequestKey\] = @originalRequestKey

ORDER BY

\[ObjectKey\],

\[ObjectTypeKey\],

\[AttributeKey\],

\[ValueString\];

/\* Which results in

[![clip_image005](http://www.ilmbestpractices.com/blog/uploaded_images/05e56e3f80a8_89E5/clip_image005_thumb.png "clip_image005")](http://www.ilmbestpractices.com/blog/uploaded_images/05e56e3f80a8_89E5/clip_image005.png)

Note that the last two rows will cause a problem with the next command because they have the same values in the objectkey, objecttypekey, attribute key and deleted columns.

Yet the adding of two values to a multi-valued string is a legal operation.

\*/

CREATE UNIQUE CLUSTERED INDEX \[IX\_ReEvaluateRequestRequestOutputStringRemovalCandidate\_ObjectKey\_ObjectTypeKey\_AttributeKey\_ValueString\]

ON #reevaluateRequestOutputStringRemovalCandidate

(

\[ObjectKey\],

\[ObjectTypeKey\],

\[AttributeKey\],

\[Deleted\]

);

/\* Resulting error:

Msg 1505, Level 16, State 1, Line 26

The CREATE UNIQUE INDEX statement terminated because a duplicate key was found for the object name 'dbo.#reevaluateRequestOutputStringRemovalCandidate\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_0000000178D0' and the index name 'IX\_ReEvaluateRequestRequestOutputStringRemovalCandidate\_ObjectKey\_ObjectTypeKey\_AttributeKey\_ValueString'. The duplicate key value is (23623, 32698, 32655, 0).

The statement has been terminated.

\*/

/\*

Then the whole transaction rolls back and the request fails

\*/

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices