---
layout: post
title: Automatic merge failed; fix conflicts and then commit the result.
---

When running **git pull** to
pull changes from a remote repository, there could well be changes in
the remote and your local repo. This causes conflits and git will fail
to merge. 








You will see the error **Automatic merge failed; fix conflicts and then
commit the result.**





****





Fortunately in git > 1.6 there is an easy fix to keep your changes
(or the remote changes) and finish the merge. Local the offending files
and run the following.










To keep the local version 










    git checkout --ours NAMEOFFILE



To keep the remote changes



    git checkout --theirs NAMEOFFILE



Then run the following to commit the changes



    git add . 

    git commit -m "merge changes"



You can now push your changes to the remote origin





 









