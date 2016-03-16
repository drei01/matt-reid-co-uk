---
layout: post
title: Android listview scrolling black
---

If you have a listview and the elements get a black background when
scrolling, **cachecolorhint**  is your saviour. Just add the following
to the listview xml file

    android:cacheColorHint="#00000000"

[Here](http://android-developers.blogspot.com/2009/01/why-is-my-list-black-android.html)
is an explanation.

Matt

 









