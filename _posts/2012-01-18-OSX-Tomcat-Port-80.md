---
layout: post
title: OSX Tomcat Port 80
---

I was recently running a webapp on tomcat that needed to run on port 80
for the links to work. This isn't easy in osx as port 80 is already
being used by other things.








The simplest way was to start tomcat on port 8080 (default) and set up
forwarding rules for port 8080 to 80 (and 8443 -> 443 for https):












*sudo ipfw add fwd 127.0.0.1,8443 tcp from any to any 443 in*







**





*sudo ipfw add fwd 127.0.0.1,8080 tcp from any to any 80 in*



 









