---
layout: post
title: OpenShift connect to mongodb local
---

I have been blogging a lot about
[OpenShift](http://openshift.redhat.com) recently because I'm finding it
a really useful PaaS for rapid development.








One issue that I have come across is connecting to mongodb on OpenShift
using my local machine. Luckily, there is a really simple fix.










Get the mongodb connection details using








``` {style="font-family: Arial, Verdana; font-size: 10pt; font-style: normal; font-variant: normal; font-weight: normal; line-height: normal;"}
rhc app-show NAMEOFYOURAPP
```








then set up port forwarding on your local machine








``` {style="font-family: Arial, Verdana; font-size: 10pt; font-style: normal; font-variant: normal; font-weight: normal; line-height: normal;"}
rhc port-forward NAMEOFYOURAPP
```








you should see something similar to the following which you can connect
to mongodb using










    mongodb 127.0.0.1:46716 =>








 









