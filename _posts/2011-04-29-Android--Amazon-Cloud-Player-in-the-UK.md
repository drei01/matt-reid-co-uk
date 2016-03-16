---
layout: post
title: Android- Amazon Cloud Player in the UK
---

Amazon's [cloud drive](https://www.amazon.com/clouddrive/learnmore) and
cloud player is an easy front end to their S3 storage solution that
allows the storage and playback of music. Combined with the [android
app](https://market.android.com/details?id=com.amazon.mp3) this makes a
neat solution to the problem of playing your music on multiple devices.
It is also cheaper than other alternatives such as dropbox (currently
$50 p/y for 50gb) and the web and android players make it ideal for my
situation. 








Having just bought a macbook pro (for my sins), I needed a way to access
my music and files across multiple devices without relying on a single
device to be **always-on**.










Setting up syncing my files to the cloud from my windows desktop was a
doddle thanks to this tutorial.




















The basics are (**Windows**):





-   Install
    [Gladinet](http://www.gladinet.com/p/download_starter_direct.htm)and
    set it up to map cloud drive to your pc.
-   Install
    [SyncToy](http://www.microsoft.com/downloads/en/details.aspx?FamilyID=c26efa36-98e0-4ee9-a7c5-98d0592d8c52)and
    set it to sync (**both** ways) your music folder and the mapped
    cloud drive.



I haven't got round the reproducing the process on my macbook yet but
**automator** that is bundled with OSX seems to be a similar offering to
SynToy.








Android App in the UK
=====================








The problem comes when I try to play my newly uploaded files from my
cloud drive on the android app. Because cloud drive is not supported in
the UK, the app detects that in the language settings and disables the
cloud playback option.








The solution
============



The solution is simple. From the home screen go to
**settings->language->locale**





and select English(US).










**If this option is not available to you, **then download the app
[morelocale2](https://market.android.com/details?id=jp.co.c_lis.ccl.morelocale) from
the android market. Create a **custom locale** and set the ISO
**country** to **US**.










After re-starting the amazon mp3 app, you should be able to sign into
your US cloud drive and play the mp3's that you have available.










Happy Days.










Matt










 









