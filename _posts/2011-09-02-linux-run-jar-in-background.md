---
layout: post
title: linux run jar in background
---

I recently needed to be able to kick off a jar file running for a batch
job in the background from a linux shell. After some googling I found
the required steps.








Save the following into your **.sh** file, replacing the jar file name










    #!/bin/bash
    nohup java -jar JARFILENAME.jar &1



 









