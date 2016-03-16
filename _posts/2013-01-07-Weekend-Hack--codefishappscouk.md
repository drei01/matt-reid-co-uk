---
layout: post
title: Weekend Hack- codefishapps.co.uk
---

I have been wanting to create a showcase site for my android apps for a
while. This weekend I decided to bite the bullet and produce an entire
site in 48 hours. Here is the result, an html5/css3 responsive site.









![](http://i46.tinypic.com/t7z8xt.png)










The site is hosted on [heroku](http://www.heroku.com), making it super
quick to push changes using the git workflow. I am using
[cloudflare](http://www.cloudflare.com) for dns (giving the site
crowd-sourced threat protection). There is a nice tutorial for
[configuring cloudflare and
heroku](http://www.ryandaigle.com/a/cloudflare-dns-heroku) by Ryan
Daigle.










The source of the site is [available on
github](https://github.com/drei01/codefish-site) thanks to a quick
[tutorial](http://blog.karlswedberg.com/pushing-an-existing-local-repo-to-new-github-repo/)
by Karl Swedberg on configuring github for an existing git project (mine
was already initialised for heroku). In short, executing the following
from the command-line works.










    git remote add origin [email protected]/*  */:youruser/remote-repo-name.git   
    git push -u origin master



The project was great fun and a great way to learn new techniques.









 









