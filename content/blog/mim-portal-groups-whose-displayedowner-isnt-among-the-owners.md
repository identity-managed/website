---
title: 'MIM Portal Groups whose displayedOwner isn''t among the Owners'
date: 2019-10-30T14:15:00.000-07:00
draft: false
url: /2019/10/mim-portal-groups-whose-displayedowner.html
tags: 
- Forefront Identity Manager
- Microsoft Identity Manager
- #FIM
- #MIM
---

In the MIM Portal it will create issues if you have a group whose displayedOwner isn't among the objects in the multivalued reference attribute Owner. Querying this through XPath is just about impossible so here is the SQL query to do it.  
  
  

SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED

GO​

USE FIMService​

GO​

  

​

SELECT DOwn.\*

FROM (​

SELECT groupObjID = G.\[objectID\]

           , GroupDisplayName = GAOVS.ValueString

           , userDisplayName= UAOVS.ValueString

           , UserObjID =  U.\[objectid\]​

FROM \[fim\].\[ObjectValueReference\] GOVR​

JOIN \[fim\].\[ObjectValueString\] GAOVS​

        ON GOVR.ObjectKey = GAOVS.ObjectKey​

JOIN \[fim\].\[Objects\] G​

          ON G.ObjectKey = GOVR.ObjectKey​

JOIN \[fim\].\[ObjectValueString\] UAOVS​

           ON GOVR.ValueReference = UAOVS.ObjectKey​

JOIN \[fim\].\[Objects\] U​

          ON U.ObjectKey = GOVR.ValueReference​

WHERE GOVR.\[AttributeKey\] =65 -- DisplayedOwner​

     AND UAOVS.\[AttributeKey\] = 1 

    AND GAOVS.\[AttributeKey\] = 1 -- DisplayedName​

) DOwn​ --DisplayedOwners

LEFT JOIN​

(​

SELECT groupObjID \= G.\[objectID\]

              , GroupDisplayName  \= GAOVS.ValueString

             , userDisplayName \= UAOVS.ValueString

             , UserObjID \=  U.\[objectid\]​

FROM \[fim\].\[ObjectValueReference\] GOVR​

JOIN \[fim\].\[ObjectValueString\] GAOVS​

        ON GOVR.ObjectKey = GAOVS.ObjectKey​

JOIN \[fim\].\[Objects\] G​

         ON G.ObjectKey = GOVR.ObjectKey​

JOIN \[fim\].\[ObjectValueString\] UAOVS​

          ON GOVR.ValueReference = UAOVS.ObjectKey​

JOIN \[fim\].\[Objects\] U​

          ON U.ObjectKey = GOVR.ValueReference​

WHERE   GOVR.\[AttributeKey\] =138 -- Owner​

        AND UAOVS.\[AttributeKey\] = 1 

        AND GAOVS.\[AttributeKey\] = 1 --DisplayedName​

) Own​ -- Owners

On Down.gObjID = Own.gObjID 

    AND Down.UObjID = Own.UObjID​

WHERE Own.UObjID IS NULL​

order by DOwn.GacctName

  

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices