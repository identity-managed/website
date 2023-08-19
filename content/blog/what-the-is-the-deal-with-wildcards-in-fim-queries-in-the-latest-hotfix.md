---
title: 'What the %_ is the deal with wildcards in FIM Queries in the latest hotfix?'
date: 2011-11-16T10:38:00.001-07:00
draft: false
url: /2011/11/ok-i-am-not-actually-swearing-nor-are.html
tags: 
- Forefront Identity Manager
- XPATH
- FIM
---

Ok I am not actually swearing, nor are those substitute words, rather % and \_ are two characters that until [hotfix rollup package (build 4.0.3594.2)](http://support.microsoft.com/kb/2520954) could be used to perform some [much needed and cool searches for sets, search scopes, groups and 3rd party client queries against FIM](http://blog.ilmbestpractices.com/2010/06/fim-sets-xpath-finding-nulls-with.html). Such as querying for the presence of string attributes.

I am sure what happened is that someone created a resource with an underscore in the name and then couldn’t search for it. So the fix. However it wasn’t broken. We need this functionality. Furthermore, simply enclosing the wildcard character in \[\] would cause it to be evaluated as a literal.

The secret, as [I previously blogged](http://blog.ilmbestpractices.com/2010/06/fim-sets-xpath-finding-nulls-with.html), is that FIM takes what you type in (on some searches) and passes it as the right hand parameter of the T-SQL LIKE operator. Ergo, whatever wildcards you can do with LIKE you can do here. Was this a form of SQL injection? Perhaps, but I tested it for other kinds of SQL injection, such as adding a single quote and other commands, and those don’t work. So it wasn’t a vulnerability, but a feature. Undocumented? Sure, but needed.

[Using Wildcard Characters As Literals](http://msdn.microsoft.com/en-us/library/ms179859.aspx)

You can use the wildcard pattern matching characters as literal characters. To use a wildcard character as a literal character, enclose the wildcard character in brackets. The following table shows several examples of using the LIKE keyword and the \[ \] wildcard characters

The problem with this hotfix is that it destroys our ability to build sets and queries that test for presence of values in string attributes. This will break many of the implementations of FIM that I and my team have done. We need a mechanism for detecting nulls in the attributes in the FIM Service database so that we can create sets based on the presence or absence of attributes.

Some might say that we can use DRE’s to accomplish this too, but the calculation of sets of objects that have DRE is non-trivial requiring the creation of an Outbound Sync Rule, the creation of a set of DRE objects, and then another set of objects whose DRL has members in the first set. But worst of all this only applies to attributes in the connector space and their matching attribute in the Metaverse and requires a few syncs and I cannot apply this approach to attributes that exist only in the FIM Service, but not in the Metaverse.

Another alternative would be to create an IsPresent function in the XPath queries, but please ensure that it works on all attribute types.

Preference of fixes (in decreasing order of desirability):

1) We can still use the wildcards in the queries, but have a way to escape them and get an IsPresent function, in other words roll back this portion of the fix and teach/document how to have the wildcards treated as literals.

2) If we can’t do that then I would prefer to see an IsPresent function in the XPath

3) If we can’t do that still use the wildcards in the queries, but have a way to escape them

Official text from [hotfix rollup package (build 4.0.3594.2)](http://support.microsoft.com/kb/2520954):

###### Issue 2

Revised the FIM "Query and Sets" features to correctly treat percent signs, underscores, and opening brackets as literals instead of as SQL wildcard characters.  
The approved character sets for strings that are used in FIM attribute values are defined in the attribute and binding schema in the FIM service. The syntax for representing an XPath filter is documented on MSDN in the following "FIM XPath Filter Dialect" article:

[http://msdn.microsoft.com/en-us/library/ee652287.aspx]( http://msdn.microsoft.com/en-us/library/ee652287.aspx) ( http://msdn.microsoft.com/en-us/library/ee652287.aspx)

Some customers may have included characters that SQL defines as query wildcard characters, such as the percent character, in FIM searches and Set filters. In this case, the customers intended FIM to treat the characters as SQL wildcard characters. This is not a documented or supported feature of the product. In some cases, customers may be able to achieve the intended functionality by removing the wildcard and by using a “contains” query/filter instead.  
Existing Set resources that have filters that contain SQL wildcard characters may not continue to function as the filters functioned before this hotfix was applied. Also, a filter that contains wildcard characters and that continued to function as expected after the hotfix was applied may function differently if the administrator later updates the filter definition.  
**Customers who used characters that SQL defined as query wildcard characters must check and revise their Set filters either before or after they upgrade to this hotfix. Customers should consider the impact of Set membership changes on Set transition MPRs**. And, customers may want to temporarily disable MPRs or update workflow definitions while they change their Set filters to avoid unintentionally triggering provisioning or deprovisioning operations during Set definition maintenance.

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices