---
layout: post
title: OpenShift zero-downtime deployment
---

OpenShift is a great PaaS for developing your webapp. When it gets to
production however, you don"t want any downtime when you are deploying.








Luckily there is a simple fix (presuming you set up a scaling app).










Find the cartridge you want to scale (**jbossews-2.0** on mine)










    rhc show-app yourapp

should show you the cartridges
    jbossews-2.0 (Tomcat 7 (JBoss EWS 2.0))  
    ---------------------------------------    
    Scaling: x2 (minimum: 2, maximum: 16) on small gears  
    haproxy-1.4 (Web Load Balancer)  
    -------------------------------    
    Gears: Located with jbossews-2.0  
    mongodb-2.2 (MongoDB 2.2)  
    -------------------------    
    Gears:          1 small    
    Connection URL: mongodb://$OPENSHIFT_MONGODB_DB_HOST:$OPENSHIFT_MONGODB_DB_PORT/   
     Database Name:  api    
    Password:       ZlRiDvsyRqcZ    
    Username:       admin



then run the following to set the minimum number of web workers to 2



    rhc scale-cartridge --a api --min 2 --max 16 -c cartridge-name





Next enable hot deployment for your app by adding the following file to
your app



    .openshift/markers/hot_deploy

 









