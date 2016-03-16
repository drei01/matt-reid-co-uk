---
layout: post
title: Bash- find the intersection and diff of 2 files
---

I recently needed to work out the intersection of 2 text files **and**
the lines that **didn't** match in 2 documents, after some googling I
found the following 2 lines of script that take 2 files and pipe the
output to a new file






#### Intersection of 2 files



    grep -Fxv -v -f all_venues distinct_venues > difference_of_files.txt

#### Difference between 2 files










    grep -Fx  -f all_venues distinct_venues > intersection.txt



 









