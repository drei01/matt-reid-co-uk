---
layout: post
title: Hack bots get 200 status
---

Since I last posted on this I have read up a bit more about the "hacks"
that I have been getting. I have also seen some requests from bots
looking to use my server as a free proxy to other sites.

The requests appear in the log as so:

``` {.js name="code"}
94.23.212.177 www.google.fr - [13/Feb/2011:12:21:18 +0000] "GET / HTTP/1.1" 200 275 "http://browseas.com/" "browseas.com telnet (MSIE compatible)"
```

They appear to have successfully managed to tunnel a url request through
my server and get the response back. After some searching, I found
[browseAs.com](http://telnet.browseas.com/telnet.php) a very useful tool
to see what response that the bot was actually getting.

``` {.js name="code"}
telnet matt-reid.co.uk 80
GET / HTTP/1.1
Host: www.google.fr
User-Agent: browseas.com telnet (MSIE compatible)
Referer: http://browseas.com/
Connection: Close




 HTTP/1.1 200 OK // The request was fulfilled. (HTTP OK)

 Connection: close
 Vary: Accept-Encoding
 Content-Type: text/html
 Accept-Ranges: bytes
 ETag: "299410394"
 Last-Modified: Tue, 01 Feb 2011 22:01:04 GMT
 Content-Length: 275
 Date: Sun, 13 Feb 2011 12:29:06 GMT
 Server: lighttpd



Matthew Reid


You are now being re-directed to the matt-reid.co.uk homepage


```

as you can see, my server was actually serving up the main index.html
page and ignoring the fact that the request it trying to get to
google.fr (i have changed the url for obvious reasons) phew!

**Note**

One thing this did bring up was that by getting a 200 response, the
attacker can see **exactly** which server and version I was using. I
have now changed this information in the config to confuse any future
potential attackers.

Matt

 









