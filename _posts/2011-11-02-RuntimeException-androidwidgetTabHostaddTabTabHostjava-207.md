---
layout: post
title: RuntimeException android.widget.TabHost.addTab(TabHost.java-207)
---

Just a quick note, I had the following exception when adding tabs to a
tabhost in an android app that I"m building








    11-03 22:54:09.530: ERROR/AndroidRuntime(508):     at android.widget.TabHost.addTab(TabHost.java:207)

The fix (after some googling) seems to be to add the following before
adding any tabs to a tabhost
    tabHost.setup();



 









