---
layout: post
title: Install Cloud9 IDE in Debian
---

I recently came across [Cloud9 IDE](http://cloud9ide.com/), a web based
code editor that allows editing of your code from anywhere via a web
browser. The IDE uses node.js and html5 features to provide a fantastic
user interface.

I decided to give it a go on my (debian based) server, here is are the
steps I took, I have included further resources at the bottom of the
page.

install git

``` {.js name="code"}
 sudo apt-get install git-core
```

install apache 2 utils (needed for node.js)

``` {.js name="code"}
 sudo apt-get install g++ curl libssl-dev apache2-utils
```

change to the directory where you want to install the ide, then run

``` {.js name="code"}
 sudo git clone git://github.com/ajaxorg/cloud9.git
```

update submodules

``` {.js name="code"}
 sudo  git submodule update --init
```

install node.js (note: compiling node.js takes the most time)

``` {.js name="code"}
 sudo su
 git clone git://github.com/ry/node.git
 cd node
 ./configure
 make
 make install
```

start cloud9 ide

``` {.js name="code"}
 node bin/cloud9.js -w /path/to/your/awesome/workspace
```

And that is it! Cloud9 IDE is now available from *http://localhost:3000*

I plan to write a full review of Cloud9 once I have used it for a while,
but here is a preview video to tempt you.

------------------------------------------------------------------------

Resources: [Installing
node.js](http://howtonode.org/how-to-install-nodejshello)

[Installing
git](http://linux.koolsolutions.com/2009/08/07/learn-git-series-part-1-installing-git-on-debian/)

[Git commands](http://help.github.com/forking/)

[Cloud9 readme](https://github.com/ajaxorg/cloud9/blob/master/README.md)

 









