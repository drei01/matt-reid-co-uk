---
layout: post
title: facebook count comments without fb-comments-count
---

Having moved my blog over to use facebook's comments plugin I needed a
new way to display the number of comments for each of my links.








It turns out to be very easy. Simply making a request to










URL_TO_COUNT_COMMENTS















returns a json string with the following format    {
       "http://www.matt-reid.co.uk/blog_post.php?id=68": {
          "id": "http://www.matt-reid.co.uk/blog_post.php?id=68",
          "comments": 1
       }
    }



 









