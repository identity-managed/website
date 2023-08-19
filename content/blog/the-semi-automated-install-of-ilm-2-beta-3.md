---
title: 'The Semi-Automated Install of ILM 2 Beta 3'
date: 2008-10-22T21:52:00.001-07:00
draft: false
url: /2008/10/semi-automated-install-of-ilm-2-beta-3.html
tags: 
- ILM
- ILM 2 Beta 3
---

ILM 2 Beta 3 won't perform a completely automatic quiet install but we can come close. Colleague Brad Turner and I have developed the following approach to the install and the post install tasks.

Brad worked out most of the issues with the ILM 2 Services install itself and then I worked on most of the issues with the post install tasks. I will cover the install of the Metadirectory services first, then the ILM 2 Beta 3 Identity Management Platform Services including its batch files and then discuss the post install tasks and present its related files.

First up the install of the Metadirectory services. At this point I assume you have covered the prerequisites mentioned in the [ILM "2" Beta 3 Installation Guide](http://technet.microsoft.com/en-us/library/cc561135.aspx) (of course we posted some of this to the community content there).

Be sure and put in your own preexisting AD groups and path to the installation folder, as well as service account and password.

InstallSync.cmd

> @echo off  
> rem This section specifies Group names, adding the domain\\ in front configures them as a domain based group  
> set GROUPADMINS="info\\ILM Admins"  
> set GROUPOPERATORS="info\\ILM Operators"  
> set GROUPACCOUNTJOINERS="info\\ILM Joiners"  
> set GROUPBROWSE="info\\ILM Browse"  
> set GROUPPASSWORDSET="info\\ILM PasswordSet"
> 
> rem ILM or DB directory?  
> set DBFileLocation=SQLDefault  
> set DBFILEMMSLOCATION="0"
> 
> rem To Use local server and instance (Default):  
> set SQLServerStore=LocalMachine  
> set SQLServerInstance=DefaultInstance
> 
> rem Installation Folder for x64  
> set INSTALLDIR64="E:\\Program Files\\Microsoft Identity Integration Server"
> 
> rem SERVICEACCOUNT is the Sync Engine Account  
> set SERVICEACCOUNT=svc.ilmsync  
> rem SERVICEDOMAIN is the domain the Sync Engine Account is in  
> set SERVICEDOMAIN=info  
> rem SERVICEPASSWORD is the password for the Sync Engine Account  
> set [SERVICEPASSWORD=P@$$w0rd](mailto:SERVICEPASSWORD=P@$$w0rd)
> 
> msiexec /i "Identity Lifecycle Manager Evaluation.msi" /norestart /log setup.txt SERVICEACCOUNT=%SERVICEACCOUNT% SERVICEDOMAIN=%SERVICEDOMAIN% SERVICEPASSWORD=%SERVICEPASSWORD% DBFILEMMSLOCATION=%DBFILEMMSLOCATION% SQLServerStore=%SQLServerStore% SQLServerInstance=%SQLServerInstance% DBFileLocation=%DBFileLocation% GROUPADMINS=%GROUPADMINS% GROUPOPERATORS=%GROUPOPERATORS% GROUPACCOUNTJOINERS=%GROUPACCOUNTJOINERS% GROUPBROWSE=%GROUPBROWSE% GROUPPASSWORDSET=%GROUPPASSWORDSET% DBFILEMMSLOCATION=%DBFILEMMSLOCATION% INSTALLDIR64=%INSTALLDIR64%

Brad and I like to use environmental variables defined in the batch file to "self-document the batch file." Since the install and the post install tend to reuse many of the same settings I moved all of the environmental variables into one batch file which is then called from the InstallSever.cmd file and the PostInstallTasks.cmd file. This file is called **SetInstallVariables.bat:**

> @echo off
> 
> set MAIL\_SERVER="mail.ensynch.info"  
> set SERVICE\_ACCOUNT\_NAME=svc.ilmws  
> set [SERVICE\_ACCOUNT\_PASSWORD=P@$$w0rd](mailto:SERVICE_ACCOUNT_PASSWORD=P@$$w0rd)  
> set SERVICE\_ACCOUNT\_DOMAIN=info  
> set SERVICE\_ACCOUNT\_EMAIL="svc.ilmws@ensynch.info"  
> set RMS\_PORT=526  
> set SERVICEADDRESS=localhost  
> set STS\_PORT=527  
> set SHAREPOINT\_PWD\_RESET\_SITE\_URL="[http://%COMPUTERNAME%/PasswordPortal/"](http://%COMPUTERNAME%/PasswordPortal/)  
> set SHAREPOINT\_SITE\_URL="[http://localhost/identitymanagement/"](http://localhost/identitymanagement/)  
> set SQLSERVER\_SERVER="."  
> set SYNCHRONIZATION\_SERVER\_ACCOUNTNQ=info\\svc.ilmma  
> set SYNCHRONIZATION\_SERVER\_ACCOUNT="%SYNCHRONIZATION\_SERVER\_ACCOUNTNQ%"
> 
> SET WSSSTSADM="%commonprogramfiles%\\microsoft shared\\web server extensions\\12\\bin\\stsadm"
> 
> SET INTIAL\_EMAIL\_ALIAS=%USERNAME%@%USERDNSDOMAIN%  
> SET INITIAL\_DESCRIPTION="%USERNAME% Initial Admin for ILM Portal"
> 
> rem Don't work...  
> set SQMOPTINSETTING=0  
> set MAIL\_SERVER\_IS\_EXCHANGE=0  
> set MAIL\_SERVER\_USE\_SSL=0
> 
> rem Shows up in the UI, but doesn't apply...  
> rem set INSTALLDIR="E:\\Program Files\\Microsoft Identity Management\\"

**The installServer.cmd file:**

> @echo off
> 
> CALL SETINSTALLVARIABLES.bat
> 
> msiexec /i ilm-server-64bit.msi /log ilmserverx64.txt ACCEPT\_EULA=1 MAIL\_SERVER=%MAIL\_SERVER% SERVICE\_ACCOUNT\_NAME=%SERVICE\_ACCOUNT\_NAME% SERVICE\_ACCOUNT\_PASSWORD=%SERVICE\_ACCOUNT\_PASSWORD% SERVICE\_ACCOUNT\_DOMAIN=%SERVICE\_ACCOUNT\_DOMAIN% SERVICE\_ACCOUNT\_EMAIL=%SERVICE\_ACCOUNT\_EMAIL% RUNNING\_USER\_EMAIL=%USERNAME%@%USERDNSDOMAIN% MAIL\_SERVER\_IS\_EXCHANGE=%MAIL\_SERVER\_IS\_EXCHANGE% MAIL\_SERVER\_USE\_SSL=%MAIL\_SERVER\_USE\_SSL% RMS\_PORT=%RMS\_PORT% SERVICEADDRESS=%SERVICEADDRESS% STS\_PORT=%STS\_PORT% SHAREPOINT\_PWD\_RESET\_SITE\_URL=%SHAREPOINT\_PWD\_RESET\_SITE\_URL% SHAREPOINT\_SITE\_URL=%SHAREPOINT\_SITE\_URL% SQLSERVER\_SERVER=%SQLSERVER\_SERVER% SQMOPTINSETTING=%SQMOPTINSETTING% SYNCHRONIZATION\_SERVER\_ACCOUNT=%SYNCHRONIZATION\_SERVER\_ACCOUNT%

After installation of ILM 2 Beta 3 you have several post install tasks per the [ILM "2" Beta 3 Installation Guide](http://technet.microsoft.com/en-us/library/cc561135.aspx):

1.  Grant Full Control rights to the ILM "2" SharePoint site to the initial user of the site
2.  Grant user rights for the ILM “2” Windows SharePoint Services site to domain users who require it
3.  Configure the ILM “2” Password Management Portal for anonymous access
4.  Disable SharePoint Indexing
5.  Exchange Server 2007 Web Service (EWS) Configuration
6.  Exchange Server 2007 Certificate installation
7.  ILM MA permissions (SQL permissions)
8.  Verify ILM Service account group membership
9.  ILM “2” Web Portal Access

For items 1 and 2 the guide provides a command line but for steps 3-9 the guide only provides steps that must be done through the GUI.

With the help of some [stsadm custom extensions](http://www.thelapointes.com/blog/Lapointe.SharePoint.STSADM.Commands.wsp) written by [SharePoint MVP Gary LaPointe](http://stsadm.blogspot.com/) we can easily automate step #3. We will use [gl-setanonymousaccess](http://stsadm.blogspot.com/2008/03/set-anonymous-access.html)

Step 4 could be automated by using the following standard stsadm command to stop the Search service

**stsadm -o osearch -action stop -f**

Or this could be handled during your WSS 3.0 install, which is how we did it. I'll have to ping another Ensynch colleague [Jeff Holliday (he calls his blog the SharePoint Redemption)](http://www.sharepointblogs.com/holliday/default.aspx)  to see how he did that when he created our install for WSS 3.0

Steps 5 and 6 are manual as is 9 (well 9 is pretty involved), but 7 (ILM MA user account SQL Permissions) is easy to automate with a SQL Script. (For the time being I am going to be lazy about step 8 -- which could be automated but which I leave as an exercise to the reader).

We need to create a login for the account we specified for the ILM 2 MA, grant it a user in the MSILM database and make it a member of the db\_owner fixed database role.

You'll see that I took advantage of sqlcmd's ability to do some preprocessing replacement using parameters or environmental variables. In this case I used environmental variables. You can see wherever it says \[$(something)\] -- like this: \[$(SYNCHRONIZATION\_SERVER\_ACCOUNTNQ)\] which is set in the SetInstallVariables.bat file

These environmental variables are set in a batch file that calls sqlcmd to execute this file: ILMMA\_Permissions.sql

> USE \[master\]  
>   
> CREATE LOGIN \[$(SYNCHRONIZATION\_SERVER\_ACCOUNTNQ)\] FROM WINDOWS WITH DEFAULT\_DATABASE=\[MSILM\]  
> GO  
>   
> USE \[MSILM\]  
> GO  
> CREATE USER \[$(SYNCHRONIZATION\_SERVER\_ACCOUNTNQ)\] FOR LOGIN \[$(SYNCHRONIZATION\_SERVER\_ACCOUNTNQ)\]  
> GO  
>   
> EXEC sp\_addrolemember N'db\_owner', N'$(SYNCHRONIZATION\_SERVER\_ACCOUNTNQ)'  
>   
> GO  
> DECLARE @myvar int  
> SELECT @myvar = (SELECT CASE  
> WHEN 1 = (SELECT COUNT(\*) FROM sys.syslogins where name = '$(SYNCHRONIZATION\_SERVER\_ACCOUNTNQ)')  
> AND 1 = (SELECT COUNT(\*) FROM sys.database\_principals WHERE name ='$(SYNCHRONIZATION\_SERVER\_ACCOUNTNQ)' )  
> AND 1 = (SELECT COUNT(\*)  
> FROM sys.database\_role\_members  
> WHERE member\_principal\_id =  
> (SELECT top 1 principal\_id FROM sys.database\_principals WHERE name ='$(SYNCHRONIZATION\_SERVER\_ACCOUNTNQ)' )  
> AND role\_principal\_id =  
> (SELECT top 1 principal\_id FROM sys.database\_principals WHERE name ='db\_owner')  
> ) THEN 0  
> WHEN 0 = (SELECT COUNT(\*) FROM sys.syslogins where name = '$(SYNCHRONIZATION\_SERVER\_ACCOUNTNQ)')  
> THEN 1 -- Couldn't create Login  
> WHEN 0 = (SELECT COUNT(\*) FROM sys.database\_principals WHERE name ='$(SYNCHRONIZATION\_SERVER\_ACCOUNTNQ)' )  
> THEN 2 -- Couldn't map user to MSILM database  
> WHEN 0 = (SELECT COUNT(\*)  
> FROM sys.database\_role\_members  
> WHERE member\_principal\_id =  
> (SELECT top 1 principal\_id FROM sys.database\_principals WHERE name ='$(SYNCHRONIZATION\_SERVER\_ACCOUNTNQ)' )  
> AND role\_principal\_id =  
> (SELECT top 1 principal\_id FROM sys.database\_principals WHERE name ='db\_owner')  
> )  
> THEN 3 -- Couldn't assign user to db\_owner role  
> ELSE 4 -- unknown error  
> END)  
> EXIT(SELECT @myvar)

Here is the PostInstallTasks.cmd file:

> @echo off
> 
> CALL SETINSTALLVARIABLES.bat
> 
> sqlcmd -S %SQLSERVER\_SERVER%  -E -i ILMMA\_Permissions.sql  
> if {%errorlevel%} == {4} (Echo  Unknown SQL Error  
>                 goto SQLPermissionsError)  
> if {%errorlevel%} == {3} (Echo  Couldn't assign user %SYNCHRONIZATION\_SERVER\_ACCOUNTNQ% to db\_owner role  
>                 goto SQLPermissionsError)  
> if {%errorlevel%} == {2} (Echo  Couldn't map user %SYNCHRONIZATION\_SERVER\_ACCOUNTNQ% to MSILM database  
>                 goto SQLPermissionsError)  
> if {%errorlevel%} == {1} (Echo  Couldn't create Login %SYNCHRONIZATION\_SERVER\_ACCOUNTNQ% On SQL Server  
>                 goto SQLPermissionsError)
> 
> echo %WSSSTSADM% -o adduser -url %SHAREPOINT\_SITE\_URL% -userlogin %USERDOMAIN%\\%USERNAME% -useremail %INTIAL\_EMAIL\_ALIAS% -username %INITIAL\_DESCRIPTION%  -role "Full Control"  
> %WSSSTSADM% -o adduser -url %SHAREPOINT\_SITE\_URL% -userlogin %USERDOMAIN%\\%USERNAME% -useremail %INTIAL\_EMAIL\_ALIAS% -username %INITIAL\_DESCRIPTION%  -role "Full Control"  
> echo Done Setting access for initial user  
> echo %WSSSTSADM% -o adduser -url %SHAREPOINT\_SITE\_URL% -userlogin "%SERVICE\_ACCOUNT\_DOMAIN%\\Domain Users" -useremail users@%USERDNSDOMAIN% -username "Domain Users" -role "Contributor"  
> %WSSSTSADM% -o adduser -url %SHAREPOINT\_SITE\_URL% -userlogin "%SERVICE\_ACCOUNT\_DOMAIN%\\Domain Users" -useremail users@%USERDNSDOMAIN% -username "Domain Users" -role "Contributor"
> 
> REM comes from here [http://stsadm.blogspot.com/2008/03/set-anonymous-access.html](http://stsadm.blogspot.com/2008/03/set-anonymous-access.html)  
> echo Using This tool from [http://stsadm.blogspot.com/2008/03/set-anonymous-access.html](http://stsadm.blogspot.com/2008/03/set-anonymous-access.html)   to set anonymous access  
> %WSSSTSADM% -o gl-setanonymousaccess -url %SHAREPOINT\_PWD\_RESET\_SITE\_URL% -anonstate entireweb  
> if {%errorlevel%} NEQ {0} goto oopsNeedCustomstsadm
> 
> goto end
> 
> :SQLPermissionsError  
> echo please  run and troubleshoot ILMMA\_Permissions.sql in SQL Management studio  
> echo remember to replace $(SYNCHRONIZATION\_SERVER\_ACCOUNTNQ) with %SYNCHRONIZATION\_SERVER\_ACCOUNTNQ%  
> goto end
> 
> :oopsNeedCustomstsadm  
> echo go download [http://www.thelapointes.com/blog/stsadm.zip](http://www.thelapointes.com/blog/stsadm.zip) then run Package\\ReleaseWSS\\deploy.bat  
> echo if the deploy.bat doesn't work then change the first line to have the .wss.wsp like so  
> echo SET SOLUTION\_NAME="Lapointe.SharePoint.STSADM.Commands.wss.wsp"
> 
> :end

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices