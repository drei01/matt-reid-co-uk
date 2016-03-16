---
layout: post
title: Java read a file as UTF-8
---

I have been writing some data import programs recently and have had
trouble with foreign characters in a text file I was reading. The
solution is in fact very simple. To create a
[BufferedReader](http://download.oracle.com/javase/7/docs/api/java/io/BufferedReader.html)
for a file in UTF-8 format, simply write the following:








    new BufferedReader(
        new InputStreamReader(
            new FileInputStream(file), UTF8));



 









