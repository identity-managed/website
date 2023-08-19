---
title: 'GUIDs to Octets, GUIDs to Base64 strings and back again'
date: 2011-12-26T12:45:00.001-07:00
draft: false
url: /2011/12/guids-to-octets-guids-to-base64-strings.html
tags: 
- PowerShell
---

  
Suppose I generate a GUID of 8c4ac332-975f-4717-ad7b-ba4a4e968fff by running the following PowerShell Command line  
  
  
  
\[system.guid\]::newguid()  
  
  
  
Don’t worry if your GUID is different from mine; it should be! If it isn’t let me know because I think I’ll partner with you for the lottery (aka a tax on the mathematically impaired).  
  
  
  
Some attributes (like the attributeSecurityGUID) when edited through ADSI Edit require you to convert the GUID to octet string (for little endian systems – Intel processors are little endian): 32c34a8c5f971747ad7bba4a4e968fff  
  
  
  
Which you can do with this one line of PowerShell script  
  
  
  
\[System.String\]::Join('',(( new-object system.guid('8c4ac332-975f-4717-ad7b-ba4a4e968fff') ).ToByteArray()  
ForEach-Object { $\_.ToString('x2') } ) )  
  
  
  
Then if you want to put this in an LDIF file you must base64 encode the value  
  
  
  
so that it looks like: MsNKjF+XF0ete7pKTpaP/w==  
  
  
  
You can do that with this one line of PowerShell  
  
  
  
\[System.Convert\]::ToBase64String((new-Object system.Guid("8c4ac332-975f-4717-ad7b-ba4a4e968fff")).ToByteArray())  
  
  
  
To convert from the Base64 string to the GUID use this line of PowerShell:  
  
  
  
new-Object -TypeName System.Guid -ArgumentList(, ( (\[System.Convert\]::FromBase64String("MsNKjF+XF0ete7pKTpaP/w==")) ) )  
  
  
  
FYI – I chose to express all of these in PowerShell as opposed to C# as many readers are not C# developers and I still wanted to give all the ability to do these transforms without the complexity of compiling code or downloading an executable.  
  
  
  
Thanks to John Geitzen whose reply to someone else’s question helped me see how to make the correct call to be able to pass the array as a whole parameter to the guid constructor instead of it getting splatted.  
  
  
  
Thanks to Poshololic whose comment on this post showed how to do the Guid to Octet conversion in one line.  
  

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices