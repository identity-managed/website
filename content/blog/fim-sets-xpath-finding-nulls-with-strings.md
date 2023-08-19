---
title: 'FIM Sets, XPATH, finding nulls with Strings'
date: 2010-06-10T00:29:00.001-07:00
draft: false
url: /2010/06/fim-sets-xpath-finding-nulls-with.html
tags: 
- Forefront Identity Manager
- XPATH
- XML
- FIM
---

A little while ago I encountered some rather strange behavior of a Set vs. the XPATH query in FIM 2010.

Using the Export-FIMConfig with the -onlyBaseResources -CustomConfig switches I run the following query to see if there are any users without a DisplayName

/Person\[not(starts-with(DisplayName,''))\]

It showed 20

So then I created a set, called “~ People with no displayname”, with that as the custom filter. I checked it doesn't violate any of the limitations listed in the [Business Policy Modeling doc](http://technet.microsoft.com/en-us/library/ff356871(WS.10).aspx) (which I must say is a pretty good doc)

Then when I look at the Set and click view members on the criteria tab it shows 20 users. So far so good

But when I go to Search for users and it Resource ID in “~ People with no displayname” it shows me over 10,000

Indeed using the commandlet to run this query /Person\[ObjectID=/Set\[DisplayName='~ People with no displayname'\]/ComputedMember\]") I get over 10,000

[Jeremy](http://social.technet.microsoft.com/Forums/en-US/ilm2/thread/64f3f2d8-17bf-4578-8b53-c95011a31edf) made a suggestion:

/Person\[not(starts-with(DisplayName,'%'))\]  

Sure enough it works both as the SET filter and as the XPATH query and showed 20 records.

So to test a string for null, use:

not(starts-wth(Attribute,'%'))

in the XPATH predicate.

**Why does this work?**

The starts-with function works just like using the [LIKE operator in T-SQL](http://msdn.microsoft.com/en-us/library/ms179859(v=SQL.105).aspx) with an implied % at the end. not(starts-wth() does a NOT LIKE '%' with the implied %. Since % will match anything as long as it is not null this effectively tests for null.

All of the wildcards available in the LIKE operator work

I have tested it using the single wildcard character \_ as well as ranges like \[a-c\] and other more complex patterns.

This also means that you can effectively do a contains in a set or group filter by doing:

starts-wth(attribute,'%searchvalue')

That’s right just prefix your searchvalue with % and what happens behind the scenes is a LIKE '%searchvalue%' which will find searchvalue anywhere in the string.

**Warning about View Members on a set (possibly groups too)**

Apparently when I click on view members on the Set’s Criteria tab it runs the XPATH query right then. But when you save the set with its new filter it runs the query in a slightly different fashion by first persisting the SET criteria to the database and then reloading the criteria and running the query and then persisting the membership results in the database to speed up look ups. (Naturally, the penalty is every create, delete, modify, add and remove request requires each set to be examined for impact and possible recalculation). So when you use the filter do do /Person\[not(starts-with(DisplayName, '%'))\] it stores that piece of the criteria as the literal string %% and the operator as LIKE. But when you use /Person\[not(starts-with(DisplayName, ''))\] it seems to delete that piece of the criteria effectively making it a set of all Persons. If you are implementing a ROPU (pronounced Rope You – Run on Policy Update) enabled workflow and this kind of thing happens to you it can me that a workflow is being applied to 10,000 objects instead of 20.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices