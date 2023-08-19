---
title: 'GUIDs to Octets, GUIDs to Base64 strings and back again'
date: 2011-12-26T12:45:00.001-07:00
draft: false
url: /2011/12/guids-to-octets-guids-to-base64-strings.html
tags: 
- PowerShell
---

#### not sure if anyone is still looking at this but i ...
[Unknown](https://www.blogger.com/profile/14935611282987980574 "noreply@blogger.com") - <time datetime="2015-01-03T04:14:01.843-07:00">Jan 6, 2015</time>

not sure if anyone is still looking at this but i have a question that seems simple but its puzzling me!  
I am trying to follow the instructions to convert a GUID into a string. I have done this:  
  
Which you can do with this one line of PowerShell script  
  
  
  
\[System.String\]::Join('',(( new-object system.guid('8c4ac332-975f-4717-ad7b-ba4a4e968fff') ).ToByteArray()  
ForEach-Object { $\_.ToString('x2') } ) )  
  
However it doesnt appear to work? how do i actually output the string?  
Thanks
<hr />
