---
title: 'Changing SQL Service Account Passwords for a Cluster'
date: 2008-10-22T13:23:00.001-07:00
draft: false
url: /2008/10/changing-sql-service-account-passwords.html
---

Here is an [excellent script for changing service account passwords](http://www.microsoft.com/technet/scriptcenter/guide/sas_ser_jpez.mspx?mfr=true) and should work fine as long as you restart the SQL services afterwards.

However the [following blog post](http://blogs.msdn.com/stuartpa/archive/2005/09/02/460363.aspx) indicates that more is going on than just a password change:  
  
"never use the plain old Windows Service Control Manager (SCM) to manipulate SQL Services.  The SQL Server Configuration Manager does a lot more work in the background to keep security consistent across the installation. "

This next blog post points out a way to change the [SQL Service Account password programmatically](http://blogs.msdn.com/mwories/archive/2006/11/03/wmi_5F00_change_5F00_password.aspx) in a way that is equivalent to use the Configuration Manager.

So here I have combined several approaches with the help of the WMI Code Creator.

My goal is to create a script that will accept a list of computers (set at the beginning of the script -- design time) and a two command line parameters, the user account and the password and then go change the password for all SQL Services on all computers listed (nodes of the cluster) that use that service account. So here it is:

' Change SQL Service Acct Passwords  
' Equivalent to using SQL Configuration Manager  
' Change passwords on multiple computers for all  
' sql services using the supplied username  
' Execute after changing the password in Active Directory  
' Ideal for Clusters  
' SQL 2005 or later  
' Copyright 2008 David Lundell  
' dlundell@ensynch.com

'1st parameter is the username domain\\user or in the case of a local user  
Set objArgs = WScript.Arguments  
If objArgs.Count <> 2 Then  
        Wscript.Echo "Usage is:"  
    Wscript.Echo "cscript SQLSvcPasswordManagement.vbs /""domain\\user"" /""NewPassword"""  
    WScript.Quit(1)  
End IF

SvcAcct = objArgs(0)  
SvcPassword = objArgs(1)

' replace the array with the list of computers in the cluster  
arrComputers = Array("mbinb2")  
For Each strComputer In arrComputers  
   WScript.Echo  
   WScript.Echo "=========================================="  
   WScript.Echo "Computer: " & strComputer  
   WScript.Echo "=========================================="

Set objWMIService = GetObject("winmgmts:\\\\" & strComputer & "\\root\\Microsoft\\SqlServer\\ComputerManagement")  
WScript.Echo  "SELECT \* FROM SqlService WHERE StartName = '" & SvcAcct & "'"  
Set ServiceCol = objWMIService.ExecQuery( \_  
    "SELECT \* FROM SqlService WHERE StartName = '" & SvcAcct & "'",,48)  
For Each objItem in ServiceCol  
    Wscript.Echo "-----------------------------------"  
    Wscript.Echo "SqlService instance"  
    Wscript.Echo "-----------------------------------"  
    Wscript.Echo "StartName: " & objItem.StartName

    Wscript.Echo "-----------------------------------"  
    Wscript.Echo "ServiceName: " & objItem.ServiceName  
ServiceName = objItem.ServiceName  
SvcType = objItem.SQLServiceType

' Obtain an instance of the the class  
' using a key property value.  
Set objShare = objWMIService.Get("SqlService.ServiceName='" & ServiceName & "',SQLServiceType='" & SvcType & "'")

' Obtain an InParameters object specific  
' to the method.  
Set objInParam = objShare.Methods\_("SetServiceAccountPassword"). \_  
    inParameters.SpawnInstance\_()

' Add the input parameters.  
objInParam.Properties\_.Item("AccountNewPassword") =  SvcPassword  
objInParam.Properties\_.Item("AccountOldPassword") =  ""

' Execute the method and obtain the return status.  
' The OutParameters object in objOutParams  
' is created by the provider.  
Set objOutParams = objWMIService.ExecMethod("SqlService.ServiceName='" & ServiceName & "',SQLServiceType='" & SvcType & "'", "SetServiceAccountPassword", objInParam)

' List OutParams  
If objOutParams.ReturnValue = 0 Then  
    WScript.Echo  ServiceName & ": Successfully changed the password"  
Else  
    WScript.Echo  ServiceName & ": failed to change the password with error code " & objOutParams.ReturnValue  
End IF  
Wscript.Echo "Out Parameters: "  
Wscript.echo "ReturnValue: " & objOutParams.ReturnValue

Next  
Next

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices