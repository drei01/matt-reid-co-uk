---
layout: post
title: Hibernate 3 transform argument type mismatch
---

I was tasked with writing a quick report from an existing sql in a
hibernate 3 and spring mvc application that I have been working on. I
decided that the quickest way to get this done would be to create a new
POJO and use the existing sql as a **named query** to transform to the
POJO in hibernate **DAO**.

This was as easy as writing:

``` {.js name="code"}
sesssion.createSQLQuery(session.getNamedQuery("examplequery")).setResultTransformer(Transformers.aliasToBean(Example.class));
```

and performing the usual operations to set the relevant parts of the
query.([More information on native sql in hibernate
here](http://docs.jboss.org/hibernate/core/3.3/reference/en/html/querysql.html))

When I came to run the application however, I got an exception:

> Caused by: java.lang.IllegalArgumentException: argument type mismatch

This was for a column that i **knew** was a string!

After some googling around I found [this blog by Michael
Scepaniak](http://tech-blog.milestoneinc.com/hibernate-argument-type-mismatch-converting-a-char-to-a-string)
detailing the problem.

It turns out hibernate isn't so good at auto-detecting data types for
native sql queries. My column was a **CHAR** not a **VARCHAR** as I had
thought.

All I had to do was **cast** the char to a varchar in the query and all
was good:

``` {.js name="code"}
select cast(char_column as varchar(32) as char_column) from some_table
```

*A slight difference from Michael's blog is that I had to specify the
number of characters (32) for the varchar in my DB2 database*

I hope this helps anyone with the same problem.

Matt

 









