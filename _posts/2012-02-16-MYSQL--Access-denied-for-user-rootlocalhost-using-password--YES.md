---
layout: post
title: MYSQL- Access denied for user ‘root’@\\\\\\'localhost’ (using password- YES)
---

While testing a new design for my site recently I came across this
error. I had been editing the mysql user"s table to let a local machine
on my network access the db temporarily.








It turns out I had accidentally overriden the
[[email protected]](cdn-cgi/l/email-protection.html)
row in the user table.










The solution can be found
[here](https://myotragusbalearicus.wordpress.com/2011/11/21/mysql-error-1045-28000-access-denied-for-user-rootlocalhost-using-password-no/) 










Stop mysql:










    sudo service mysql stop

Start with skip-grant-tables     cd /usr/bin sudo mysqld_safe --skip-grant-tables

Open a new terminal windowUpdate the user    $mysql 

    mysql> use mysql;

    mysql> UPDATE user SET Host="localhost" WHERE user = "root" and Host="WHATITWASBEFORE";

    mysql> exit;

Kill the safe mode version of myslq    ps -ef | grep mysql

    sudo kill -9 PROCESS_ID_OF_MYSQL

Start mysql again:
    sudo service mysql start




 









