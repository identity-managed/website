---
title: 'ILM 2 Functions Explained'
date: 2009-01-06T13:08:00.001-07:00
draft: false
url: /2009/01/ilm-2-functions-explained.html
tags: 
- ILM
- ILM 2 RC0
---

Function Name

Parameters

David's Description

Example

Example Explanation

BitAnd

1) mask  
Type: Integer  
  
2) flag  
Type: Integer

BitAnd is a bitwise operation anding **mask** and **flag**. So if **Flag** is the UserAccountControl Attribute in AD and **mask** is negative 2147483645 (the [two's complement](http://mathforum.org/library/drmath/view/54344.html) of 2) Then the result is that the disable bit (bit 2) is turned off leaving all of the other bits unchanged.  
  
  
  
  
  
  
  
BitAnd can be combined with Eq to detect if a bit is set

BitAnd(-2147483645 , userAccountControl)   
  
  
BitAnd(-2147483645 , 514) =512  
  
  
BitAnd(-2147483645 , 512) =512  
  
  
BitAnd(-2147483631 , 528) =512  
  
BitAnd(-2147483631 , 512) =512  
  
Eq( BitAnd(2,userAccountControl),2)

Turn off the disable bit Flow the result into [userAccountControl](http://msdn.microsoft.com/en-us/library/ms680832(VS.85).aspx) in AD to enable a user.  
  
if userAccountControl is 514 then the example gives us 512,  
  
if it is 512 then it remains unchanged.  
  
To figure out what to use as the mask we first start with what bit we want to set bit 16 -- account is locked out) then take the [two's complement](http://mathforum.org/library/drmath/view/54344.html) (start with negative of (2^31 -1)  
\-2147483647 and add the value of the bit, in this case 16 to give us -2147483631)  
  
If that is true then the disable bit is currently set in AD

BitOr

1) mask  
Type: Integer  
  
2) flag  
Type: Integer

BitOr is a bitwise operation ORing **mask** and **flag**. So if **Flag** is the UserAccountControl Attribute in AD and **mask** is 2 Then the result is that the disable bit is turned on

BitOr(2, userAccountControl)  
  
BitOr(2, 512) = 514  
  
BitOr(2, 514) = 514  
  
  
  
  
Doesn't work ([vote on this feedback](https://connect.microsoft.com/feedback/ViewFeedback.aspx?FeedbackID=391175&SiteID=433)):  
BitOr(  
IIF( Eq(scope,"Universal"),8,IIF(Eq(scope,"DomainLocal"),4,IIF(Eq(scope,"Global"),2,0)))  
, IIF(Eq(type,"Distribution"),0,2147483648)  
)

Turn on the disable bit. Flow the result into userAccountControl in AD to disable a user.    
if userAccountControl is 512 then the example gives us 514.  
if it is 514 then it remains unchanged.   
  
  
returns an error of "return type (Object) of function IIF is not Integer"

CRLF

None

puts in a Carriage return line feed

CRLF()="  
"  
"Fred"+ CRLF() + "Flatstone" =  
"Fred  
Flatstone"

The only function with no parameters but it still needs the () otherwise ILM thinks you are looking for an attribute.

DateTimeFormat

1)dateTimeString  
Type:String  
  
2)format  
Type:String

Take the date and time in the **dateTimeString** and format it according to the **format** parameter. As far as I have tested it works according to [Standard Date Time Formats](http://msdn.microsoft.com/en-us/library/az4se3k1.aspx) and .[NET Custom Date and Time Format Strings](http://msdn.microsoft.com/en-us/library/8kb3ddd4.aspx)

DateTimeFormat("12-28-2008 12:34:01.213 PM", "MM/dd/yyyy  ddd dddd hh:mm:ss  d  f M") ="12/28/2008 ;Sun ;Sunday ;  
12:34:01 ;28 ;2 ;12"  
  
DateTimeFormat("12-28-2008 12:34:01.213 PM", "G")  ="12/28/2008 ;12:34:01 ;PM"

It looks like you can use either the custom strings (like MM/dd/yyyy) or standard strings (like G)

ConvertSidToString

1) ObjectSID  
Type:Binary

I suppose that this one works just like our good old [Utils.ConvertSidToString method in the Metadirectory namespace](http://msdn.microsoft.com/en-us/library/ms698815(VS.85).aspx)  
and is used to convert a SID to a string

EscapeDNComponent

1) dnStr  
Type:String

Again I suppose this one works just like  
[ConnectedMA.EscapeDNComponent](http://msdn.microsoft.com/en-us/library/ms696769(VS.85).aspx)

EscapeDNComponent("CN=Turner, Brad") = "CN=Turner\\, Brad"

The function will escape out characters that are not permitted in distinguished names (this will vary MA by MA)

IIF

1)condition  
Type:Boolean  
  
2)valueTrue  
Type: Object  
  
3)valueFalse  
Type: Object

If **condition** is true then return **valueTrue** if condition is false return **valueFalse**

IIF(Eq(1,1), "Yes it's true", "No it's false") = "Yes it's true"  
  
IIF(Eq(1,2), "Yes it's true", "No it's false") = "No it's false"  
  
IIF(Eq(type,"Distribution"),  
IIF(Eq(scope,"Universal"),8,  
IIF(Eq(scope,"DomainLocal"),4,  
IIF(Eq(scope,"Global"),2,0))),  
IIF(Eq(scope,"Universal"),-2147483640,IIF(Eq(scope,"DomainLocal"),-2147483644,IIF(Eq(scope,"Global"),-2147483646,0))))

  
  
  
  
  
  
[Example Brad and I cooked up](http://www.identitychaos.com/search?q=grouptype) for group translating the string attributes type, and scope into an integer which we then flowed into the AD group attribute [groupType](http://msdn.microsoft.com/en-us/library/ms675935(VS.85).aspx) which combines group scope with whether it is a distribution list or not.

Left

1) str  
Type:String  
2) numchars  
Type:Integer

Get a substring of **str** starting at the left and going **numChars** long

Left("David Lundell",5)="David"

LowerCase

1) str  
Type:String

The name says it all

LeftPad

1) str  
Type:String  
2) length  
Type:Integer  
3)padCharacter  
Type:String

According to my testing this function works like LeftPad in the String Utils library in [**org.apache.commons.**](http://commons.apache.org/lang/api/org/apache/commons/lang/StringUtils.html#leftPad(java.lang.String, int, char))  
take **padcharacter** and add it to the beginning of **str** until **str** is as long as **length**. If **str** is already as long as or longer than **length** then don't pad.

LeftPad("David",3,"a")="David"  
LeftPad("David",6,"a")="aDavid"  
LeftPad("David",8,"a")="aaaDavid"  
LeftPad("David",-1,"a")="David"

LeftPad and RightPad will never truncate or overwrite the original **str**

Mid

1)str  
Type: String  
2)pos  
Type: String  
3)numChars  
Type: Integer

Get a substring of **str** starting at **pos** and going for **numChars**.

Mid("Brad ILM Turner",3,5) = "ad IL"

LTrim

1) str  
Type:String

Remove leading whitespace

LTrim("  Fred Mitchell  ") = "Fred Mitchell  "

ProperCase

1) str  
Type:String

Capitalize the first letter of every word (presumably words are determined by having whitespace in between them)

ProperCase("david lundell") = "David Lundell"  
ProperCase("David lundell") = "David Lundell")  
ProperCase("DAVID lundell") = "David Lundell")

RandomNum

1)start  
Type:Integer  
2)end  
Type:Integer

Generate a random Integer in between (inclusive) **start** and **end**

RandomNum(10,15) = ? where ? is between 10 and 15 (inclusive)

Right

1) str  
Type:String  
2) numchars  
Type:Integer

Get a substring of **str** starting at the Right going **numChars** long

Right("David Lundell",5) = "ndell"

Trim

1) str  
Type:String

Remove leading and trailing whitespace

Trim("  Fred Mitchell  ") = "Fred Mitchell"

I haven't tested all of the whitespace characters like CRLF

RTrim

1) str  
Type:String

Remove trailing whitespace

RTrim("  Fred Mitchell  ") = "  Fred Mitchell"

RightPad

1) str  
Type:String  
2) length  
Type:Integer  
3)padCharacter  
Type:String

According to my testing this function works like RightPad in the String Utils library in **[org.apache.commons](http://commons.apache.org/lang/api/org/apache/commons/lang/StringUtils.html#rightPad(java.lang.String, int, char))**  
take **padcharacter** and add it to the end of **str** until **str** is as long as **length**. If **str** is already as long as or longer than **length** then don't pad.

RightPad("David",3,"a")="David"  
RightPad("David",6,"a")="Davida"  
RightPad("David",8,"a")="Davidaaa"  
RightPad("David",-1,"a")="David"

LeftPad and RightPad will never truncate or overwrite the original **str**

UpperCase

1) str  
Type:String

Self-Explanatory

Word

1) str  
Type:String  
2)wordIndex  
Type:Integer  
3)delimiters  
Type:String

Take **str** and chop it up into words based **delimiters**, and then return the 1st, 2nd, 3rd, 4th etc word based on **wordIndex**

Word("Brad;ILM,Turner",2,";,") = "ILM"  
Word("Brad;ILM;Turner",2,";") = "ILM"  
Word("Brad;,ILM;,Turner",2,";,")=""  
Word("Brad;,ILM;,Turner",3,";,") = "ILM"  
Word("Brad;ILM,Turner",3,";,")="Turner"

**delimeters** takes each delimiter character and uses them as separate delimitters not as a combination delimitter so ";," means that the second word in "Brad;,ILM;,Turner" is "" and the third word is "ILM"

Hopefully this helps you in your codeless provisioning quest.  
Remember there are limitations like the output of IIF can't feed into a function parameter expecting an Integer like the mask or the flag in BitAND or BitOR -- and no, I am not BitOr about it. Without casting and conversion functions that is an obstacle that can't be overcome using the ILM 2 functions for that you may need to turn to [custom workflows](http://www.identitychaos.com/2008/12/ilm-2-rc0-workflow-activity-walkthrough.html).

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices