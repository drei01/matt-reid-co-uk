---
layout: post
title: Ubuntu 10.04 DVD playback
---

I have just managed to get DVD"s to play in Ubuntu after a lot of
googling and these tutorials
([here](http://ubuntuforums.org/showpost.php?p=7197110&postcount=5) and
[here](http://superuser.com/questions/53905/dvd-wont-play-in-ubuntu-jaunty-after-codes-and-css-support-has-been-added)).Here goes:
-   Run the following in the Terminal
``` {.js name="code"}
sudo wget http://www.medibuntu.org/sources.list.d/jaunty.list --output-document=/etc/apt/sources.list.d/medibuntu.list 
```

``` {.js name="code"}
sudo apt-get update && sudo apt-get install medibuntu-keyring && sudo apt-get update
```

``` {.js name="code"}
sudo apt-get install libdvdcss2                 
```

``` {.js name="code"}
sudo apt-get install w32codecs                   
```

``` {.js name="code"}
sudo apt-get install libdvdread4                 
```

``` {.js name="code"}
sudo /usr/share/doc/libdvdread4/install-css.sh
```

``` {.js name="code"}
sudo apt-get install ubuntu-restricted-extras                   
```

-   This will install the codecs you need to get DVDs to play.
-   Then run the following to set the region of the DVDs you wish
    to play.

    sudo apt-get install regionset

    sudo regionset

and change the region to the number you want (1-4)-   Finally install MPlayer (the only player I could get DVDs to work
    with successfully).

Click:Applications ->Ubuntu Software CenterThen search for:GNOME mplayer 









