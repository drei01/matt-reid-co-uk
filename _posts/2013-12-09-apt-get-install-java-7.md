---
layout: post
title: apt-get install java 7
---



Installing java 7 is a simple process in linux (debian etc). Follow
these simple steps to get it installed.



    sudo su
    echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu precise main" | tee -a /etc/apt/sources.list
    echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu precise main" | tee -a /etc/apt/sources.list
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886
    apt-get update
    apt-get install oracle-java7-installer
    exit



To set Java 7 as the default version run (you may have to sudo):



    apt-get install oracle-java7-set-default



And run the following to check the java version



    java -version

 









