---
layout: post
title: DB2 select distinct with order by
---

Today I had to select a distinct column on a DB2 table but I also wanted
the query ordered. When I tried *select distinct title from product
order by price, qty* the sql compiler complained that it didn't
recognise the *order by* statement.

After a while of googling the problem, IBM came to the rescue. I found
[this
page](http://publib.boulder.ibm.com/infocenter/db2luw/v8/index.jsp?topic=/com.ibm.db2.udb.doc/admin/r0000879.htm)
detailing how a achieve the desired result using a *WITH* statement
(which I seem to be using a lot recently..).

So the correct syntax to order a distinct select in DB2 is

``` {.js name="code"}
with PRODUCT(title){
    select distinct title from products
}

select title from PRODUCT order by price,qty
```

I hope this helps anyone else who come across the same problem

Matt

 









