---
layout: post
title: git push all
---

When working on a project using git for version control, it may be
useful to be able to push changes to multiple remotes (for example
heroku and github at once).








Luckily it"s very simple. Edit **.git/conf** and add



    [remote "all"]    
        url=ssh:[email protected]/*  *//repos/g0.git    
        url=ssh:[email protected]/*  *//repos/g1.git

 replacing g0 and g1 with the urls for your repositories.

Push your changes to all repos with



    git push all

 









