---
layout: post
title: JQuery Fibonacci Tree
---

I was recently questioned by [Hannah
Suppiah](http://hannahsuppiah.blogspot.com/) about writing code to
calculate fibonacci numbers and it brought my uni days flooding back. As
an illustrative tool and a quick bit of nostalgia, I wrote this simple
JQuery example of the fibonacci tree.

There 2 lines of JQuery needed to work out the n'th fibonacci number.

``` {.js name="code"}
function fib(n){
      if(n<=1){//if we are trying to get the first number then return it        
        return 1;
      }                           
      //otherwise return the sum of the last 2
      return fib(n-1)+fib(n-2);
    }
```

Because a fibonacci number is defined as the sum of the previous 2, as
simple bit of recursion is required to calculate it (re-cursing down
until we get to a known value [i.e 1]).

 









