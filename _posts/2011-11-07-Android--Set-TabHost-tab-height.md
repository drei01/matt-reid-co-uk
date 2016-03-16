---
layout: post
title: Android- Set TabHost tab height
---

I recently found the following post on stackoverflow
[here](http://stackoverflow.com/questions/4768173/dont-want-icons-on-my-tabwidget/4768644#4768644),
simply add the following code (sorry, no xml version)








    tabHost.getTabWidget().getChildAt(0).getLayoutParams().height = 25;

If you have your tabs positioned at the bottom of the screen, make sure
you give **android:gravity="bottom"** to your layout



 









