---
layout: post
title: PHP mobile device detection
---

With the latest version of this site, I decided to try and cater for
mobile devices as well as desktop browsers.

I came across [php mobile
detect](http://code.google.com/p/php-mobile-detect/), an open source php
class for easy detection of various mobile devices on your php site.

Detection is as easy as writing the following lines at the top of your
include script:

``` {.js name="code"}
include("Mobile_Detect.php");$detect = new Mobile_Detect.php();
```

followed by

``` {.js name="code"}
if ($detect->isMobile()) {   
 // any mobile platform
}
```

anywhere you want to check for mobile devices.

I am using this script to serve a simplified mobile stylesheet instead
of the standard style to mobile devices (i hope to add features such as
[jquery mobile](http://jquerymobile.com/) in the future)

Matt

 









