---
layout: post
title: jQuery fadeout and remove
---

Animation can be a bit of a hassle with jQuery, especially when you want
to chain an animation and another action (such as removing the element
from the DOM). The animation can often get missed out in the sequence of
events.








The key to solving this is to use jQuery's
[queue()](http://api.jquery.com/jQuery.queue/)functionality.










Here's a quick demonstration:













 









