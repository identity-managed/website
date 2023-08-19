---
title: 'Revisiting GUIDs, Octets and Base64'
date: 2012-12-02T20:59:00.001-07:00
draft: false
url: /2012/12/revisiting-guids-octets-and-base64.html
tags: 
- AD LDS
- AD
- LDAP
---

After re-reading my [earlier post](http://blog.ilmbestpractices.com/2011/12/guids-to-octets-guids-to-base64-strings.html) on this subject I decided I could be clearer.

GUIDs are often used in three different formats:

**Representation**

**Example**

Canonical form

8c4ac332-975f-4717-ad7b-ba4a4e968fff

Octet String

32c34a8c5f971747ad7bba4a4e968fff

Base64 Encoded

MsNKjF+XF0ete7pKTpaP/w==

**Representation**

**Comment**

**Used in**

Canonical form

This format stems from the way GUIDs (UUIDs) are generated. Each dash separating the various components. In version one of the [UUID specification](http://www.ietf.org/rfc/rfc4122.txt), the first the last component was the MAC address of the computer that generated the GUID.

Most places

Octet String

This shows the GUID in [little Endian](http://en.wikipedia.org/wiki/Little_endian#Little-endian) order. In essence the first three groups had their bytes listed in reversed order and the dashes removed. The last two groups did not get switched.  
So the 8c4ac332 became 32c34a8c, the 975f became 5f97  
and 4717 became 1747. The last two components remained the same.

**ADSI Edit** when changing certain attributes like attributeSecurityGUID which is used for assigning permissions to attributes

Base64 Encoded

This is the [Base64 encoding](http://en.wikipedia.org/wiki/Base64) of the OctetString and is the most compact of the three forms (Depending on the Padding, GUIDs in BASE64 are 22 to 24 characters in length)

**LDIF files** for all GUID attributes (at least all of them that I recall)

PowerShell Code Snippets

**To Generate a new GUID (with a new random number)**

Code:

\[system.guid\]::newguid()

Output (you out should vary. If it doesn't call me and we can explore other mathematical improbabilities together, like the winning lottery numbers -- actually I don't play and neither should you):

8c4ac332-975f-4717-ad7b-ba4a4e968fff

**To Convert from the canonical form to Octet String (for ADSI Edit for some attributes)**

Code (put your GUID inside the parenthesis replacing mine):

\[System.String\]::Join('',(( new-object system.guid('8c4ac332-975f-4717-ad7b-ba4a4e968fff') ).ToByteArray() | ForEach-Object { $\_.ToString('x2') } ) )

Output:

32c34a8c5f971747ad7bba4a4e968fff

**To Convert from the canonical form to Base64 Encoded (for use in LDIF files)**

Code:

\[System.Convert\]::ToBase64String((new-Object system.Guid("8c4ac332-975f-4717-ad7b-ba4a4e968fff")).ToByteArray())

Output

MsNKjF+XF0ete7pKTpaP/w==

**To Convert from Base64 Encoded to Canonical form**

Code:

new-Object -TypeName System.Guid -ArgumentList(, ( (\[System.Convert\]::FromBase64String("MsNKjF+XF0ete7pKTpaP/w==")) ) )

Output

8c4ac332-975f-4717-ad7b-ba4a4e968fff

FYI – I chose to express all of these in PowerShell as opposed to C# as many readers are not C# developers and I still wanted to give all the ability to do these transforms without the complexity of compiling code or downloading an executable.

Thanks to [John Geitzen](http://stackoverflow.com/users/57986/john-gietzen) whose [reply to someone else’s question](http://stackoverflow.com/questions/5172134/base64-to-guid-to-base64) helped me see how to make the correct call to be able to pass the array as a whole parameter to the guid constructor instead of it getting splatted.

Thanks to Poshololic whose comment on [this post](http://www.leadfollowmove.com/archives/powershell/converting-a-guid-string-to-octet-string) showed how to do the Guid to Octet conversion in one line. 

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices