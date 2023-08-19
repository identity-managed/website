---
title: 'FIM Custom Expressions inside Custom Expressions?'
date: 2015-11-09T10:16:00.000-07:00
draft: false
url: /2015/11/fim-custom-expressions-inside-custom.html
tags: 
- Forefront Identity Manager
- FIM 2010 R2
- Microsoft Identity Manager
- MIM
- Sync Rules
- FIM
---

Recently, I needed to take Longitude and Latitude data that was given to me in the following format and break it into its individual components and then flow it out to AD.  
Let's suppose the data looks like this:  

"Point -10.1223 45.945"

I could just use the Left and Right functions to get out the Longitude and Latitude.

  

The problem was it could also look like this depending on the level of precision:

"Point -10.1223453333 45.945111113" 

  

So using the Left and Right functions were right out.

  

But I could use the Word function

Word(GeoData,2," ") gives me -10.1223 for the first row and -10.1223453333 for the 2nd row

Word(GeoData,3," ") gives me 45.945 for the first row and for the 2nd: 45.945111113

  

Suppose the data was slightly different a comma instead of space in between.

"Point -10.1223,45.945"

"Point -10.1223453333,45.945111113"

  

Now I can add another delimiter in addition to the space character I can put in a comma:

Word(GeoData,2," ,") gives me -10.1223 for the first row and -10.1223453333 for the second row

Word(GeoData,3," ,") gives me 45.945 for the first row and for the second: 45.945111113

  

Let's add another twist (which gets to how the data was really presented) and put the data inside parenthesis like so:

"Point (-10.1223 45.945)"

"Point (-10.1223453333 45.945111113)" 

  

But when I tried to do 

Word(GeoData,3," (")

I got an error "the function Word is not correctly formatted"

[![](http://2.bp.blogspot.com/-SsxRIS0aStQ/VkDRlLtxR0I/AAAAAAAAAH4/tef1-Zxx04Y/s400/The%2Bfunction%2BWord%2Bis%2Bnot%2Bcorrectly%2Bformatted.png)](http://2.bp.blogspot.com/-SsxRIS0aStQ/VkDRlLtxR0I/AAAAAAAAAH4/tef1-Zxx04Y/s1600/The%2Bfunction%2BWord%2Bis%2Bnot%2Bcorrectly%2Bformatted.png)

Then I had a brain storm! What about putting a CustomExpression inside a CustomExpression?

[![](http://3.bp.blogspot.com/-ND6Qtfpy2q8/VkDR25YxqhI/AAAAAAAAAIA/fIWxFSSdh6U/s400/CustomExpression%2Bcould%2Bnot%2Bbe%2Blocated.png)](http://3.bp.blogspot.com/-ND6Qtfpy2q8/VkDR25YxqhI/AAAAAAAAAIA/fIWxFSSdh6U/s1600/CustomExpression%2Bcould%2Bnot%2Bbe%2Blocated.png)

Bummer: "The function named CustomExpression could not be located" so no nesting of Custom Expressions!

  

So for giggles I decided to not start it with a customExpression

  

[![](http://1.bp.blogspot.com/-KCxhaPxMePw/VkDST9xJXwI/AAAAAAAAAII/3nPxy0EuP84/s640/Word%2Bnot%2Bcustomexpression.png)](http://1.bp.blogspot.com/-KCxhaPxMePw/VkDST9xJXwI/AAAAAAAAAII/3nPxy0EuP84/s1600/Word%2Bnot%2Bcustomexpression.png)

  

That worked!

  

So the lesson is that sometimes trying to use some of the special characters, like a parenthesis inside of a literal string confuses the CustomExpression parser but can work when put inside the parameter of the function call (not inside the Custom Expression)

  

I did indeed confirm that the parenthesis was the problem as it worked with other characters just not a literal parenthesis when doing a whole custom expression.

  

http://feeds.feedburner.com/IdentityLifecycleManagerilmBestPractices