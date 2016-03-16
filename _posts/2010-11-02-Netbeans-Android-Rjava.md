---
layout: post
title: Netbeans Android R.java
---

Anyone using the [nbandroid](http://en.androidwiki.com/wiki/NetBeans)
plugin for netbeans to develop android apps may have come accross the
same problem I did.

R.java doesn't seem to get updated.

In order to fix this, add the following lines to the AnroidManifest.xml
and 'build' the project again.

``` {.js name="code"}
 
   Generating R.java / Manifest.java from the resources...
   
     
     
     
     
     
     
     
     
     
     
   
 
```

R.java is magically updated

Matt

 









