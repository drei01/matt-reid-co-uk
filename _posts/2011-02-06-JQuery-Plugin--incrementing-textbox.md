---
layout: post
title: JQuery Plugin- incrementing textbox
---

I recently needed to increment and decrement a number inside a textbox
using jQuery and couldn't find a decent solution online. I decided to
create my own generic plugin so I can re-use it where ever I see fit.

I have made the plugin as generic as possible so it is mark-up
independent and you can use any element. I have also added the ability
to limit the range of the input (the reason I created it in the first
place)

**Demo**

loading..
**Code**

Here is the plugin code in full

``` {.js name="code"}
 /*  
  @author: Matthew Reid
  @date: 07/02/2011
  jQuery plugin to incrememnt the numeric value of an element
  Example usage:
    +
    -
    
    
      $(function(){
        $('#numeric&#95;value').incrementBox({minVal:0,maxVal:30});
        });
    Option:
      minVal - the lowest possible value
      maxVal - the highest possible value
      incButton - selector for the increment button
      decButton - selector for the decrement button
  */
    (function($){

        $.fn.extend({
            incrementBox: function(options) {

                var defaults = {
                    minVal:null,
                    maxVal:null,
                    incButton:'#inc',
                    decButton:'#dec'
                }

                var getNumVal = function($element){//get numeric value of an object
                                  var value = Number($element.val());
                                  return isNaN(value) ? 0 : value;
                                }
                var correctValue = function(min, max, value){
                  var checkMin = min!=null && !isNaN(0+min);
                  var checkMax = max!=null && !isNaN(0+max);
                  if(value>max && checkMax){
                    return max;
                  }
                  if(value<min && checkMin){
                    return min;
                  }
                  return value;
                }

                var options =  $.extend(defaults, options);

                return this.each(function() {
                    var o = options;
                    var $obj = $(this);
                      $(o.incButton).click(function(){                       
                        $obj.val( correctValue(o.minVal, o.maxVal, (getNumVal($obj) + 1)) );
                      });
                      $(o.decButton).click(function(){                               
                        $obj.val( correctValue(o.minVal, o.maxVal, (getNumVal($obj) - 1)) );
                      });
                      $obj.blur(function(){
                        $obj.val( correctValue(o.minVal, o.maxVal, getNumVal($obj)) );
                      });                   
                });
            }
        });

    })(jQuery);
```

Feel free to re-use any part of this code.

Matt

**Known Issue:**
This plugin will not work out of the box when placed in a form. Add:

``` {.js name="code"}
onclick="return false;"
```

in order to stop the form getting submitted every time a button is
clicked
 

<div>



</div>



</div>

<div class="post-footer cf">

<div class="back-to-top cf">

[<span>Back to top</span>](blog_post.php-id=46.html#content)

</div>

-   Tags: [jquery](search.php-category=jquery.html),
    [plugin](search.php-category=%20plugin.html),

</div>

</div>

</div>

</div>

</div>

</div>

##### Connect with me {#contact}

[![](images/icons/twitter.png)](http://twitter.com/Matthew_Reid "Twitter")
[![](images/icons/github.png)](http://github.com/drei01 "Github")
[![](images/icons/linkedin.png)](http://linkedin.com/e/fpf/70699506 "Linkedin")
©2016 [matt-reid.co.uk](index.html)

</div>
