---
layout: post
title: Postgres like multiple words
---

When using
postgres, we sometimes need to find fields that match multiple
**like** queries. 









In this situation we can use **like
any**. Making use of the
[any](http://www.postgresql.org/docs/9.2/static/functions-comparisons.html)
expression.











Example:





    select * from some_table where some_field like any  (
        select '%'||some_other_field||'%' from some_other_table
    );



 









