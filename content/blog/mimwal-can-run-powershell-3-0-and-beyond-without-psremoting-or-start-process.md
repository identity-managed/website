---
title: MIMWAL Can run PowerShell 3.0 and beyond without PSRemoting or Start-Process!
description: |-
  How to run more than just PowerShell 2.0 in MIMWAL without
    PowerShell remoting or Starting a new Process
tags:
  - MIMWAL;MIM;PowerShell
date: 2024-06-07T17:11:48.628Z
banner: /img/mimwal-powershell_uselegacyv2runtimeactivationpolicy.png
---
I﻿ just discovered that a colleague had several years prior managed to get MIMWAL PowerShell Activity to run Get-ADUser and other commandlets from the Active Directory Module (which requires PowerShell 3.0 or later) without  using PowerShell Remoting or starting a new Process with Start-Process.

**<﻿Caution> Per [Eugene Sergeev](https://www.facebook.com/groups/155109068156/user/100005144859467/?__cft__[0]=AZU68Ki5NtCqdDbhcJmXXMYH8jS70-NO2zLap5YaNYuaOFl7mzJBGdzi89MwYPFF35dsLKgj4OXk-RZp700DisXsm3m0EluUUkEhoxsHvnNh0JbeaaLM7l1s_dz3Ck5kA2LYKOc-unW9KRmyS-C4M-_TtwyYi102Ov6RG-aWYRFUCA6k1iSfK6KR6iDFe3BtO7lQLN-Q2NEHN_B3EctAZBIE&__tn__=R]-R)**

> This breaks SSPR AuthN workflows.

**<﻿/Caution>**

S﻿o if you aren't using SSPR through MIM this might be an option for you!

According to the [MIMWAL Wiki](https://github.com/Microsoft/MIMWAL/wiki/Run-PowerShell-Script-Activity)

> If there is a need to execute a script containing PowerShell 3.0+ cmdlets (e.g. ActiveDirectory module on Windows Server 2012), they can be made to run in a separate process to avoid the product limitation. e.g. using PowerShell Remoting or launching a new "powershell.exe" session using `Start-Process` cmdlet

But this is not quite true. The trick is in the Microsoft.ResourceManagement.Service.exe.config file.

According to a Microsoft Learn Article the useLegacyV2RuntimeActivationPolicy:

> Specifies whether to enable the .NET Framework 2.0 runtime activation policy or to use the .NET Framework 4 activation policy.
>
> Enable .NET Framework 2.0 runtime activation policy for the chosen runtime, which is to bind legacy runtime activation techniques (such as the [CorBindToRuntimeEx function](https://learn.microsoft.com/en-us/dotnet/framework/unmanaged-api/hosting/corbindtoruntimeex-function)) to the runtime chosen from the configuration file instead of capping them at CLR version 2.0. Thus, if CLR version 4 or later is chosen from the configuration file, mixed-mode assemblies created with earlier versions of the .NET Framework are loaded with the chosen CLR version. Setting this value prevents CLR version 1.1 or CLR version 2.0 from loading into the same process, effectively disabling the in-process side-by-side feature.

P﻿ut the following in  Microsoft.ResourceManagement.Service.exe.config file just before the runtime tag

 `<startup useLegacyV2RuntimeActivationPolicy="true">
    <supportedRuntime version="v4.0"></supportedRuntime>
    <supportedRuntime version="v2.0.50727"></supportedRuntime>
  </startup>`

R﻿emember to restart your Forefront Identity Manager Service before you expect it to work.

I﻿ ran the following script:

`$PSVersionTable.PSVersion | Out-File -FilePath "D:\FIMLog\Disabled_account_memberof\2024\test.txt"
import-module ActiveDirectory
GEt-aduser "Dlundell" | out-file -FilePath "D:\FIMLog\Disabled_account_memberof\2024\testgetaduser.txt"`

And got the following output:

Major  Minor  Build  Revision

- - -

5      1      20348  2400  

DistinguishedName : CN=David Lundell (DLundell),OU=Client Consultants,DC=Clientlab,DC=local
Enabled           : False
GivenName         : David
Name              : David Lundell (DLundell)
ObjectClass       : user
ObjectGUID        : <Obscured>
SamAccountName    : DLundell
SID               : <Obscured>
Surname           : Lundell
UserPrincipalName : DLundell@Clientlab.local