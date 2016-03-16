---
layout: post
title: Jquery autocomplete and webatu.com
---

I am using webatu.com as a host for this site (because it is free and
gives my php and myql).Hopefully one day I will actually be able to afford to get some real
hosting but this will do for now. I have had no problems with it at all
fingers crossed.I was wondering for ages why the autocomplete on my searchbox wasn't
firing properly(jquery loves to fail silently not giving you any trace
at all). I checked the GET requests and noticed that the JSON string
that my search file was returning was getting some html comment tags
added to it by webatu so jquery wasn't recognising it as proper JSON and
so was failing.Here is the fix:

``` {.js name="code"}
var $search = $('#search');//Cache the element for faster DOM searching since we are using it more than once
            //set up autocompletion of searches (a very long way to get round webatu adding html comments to everything)
            $search.autocomplete({
                    minLength: 2,
                    source: function(request, response) {
                        if ( request.term in cache ) {
                            response( cache[ request.term ] );
                            return;
                        }
                                                $.ajax({
                            url: "/includes/tags.php",
                            dataType: "html",
                            data:request,
                            success: function( data ) {
                                //todo:avoid running 3 seperate regex
                                data = data.replace(/ )]+-->/g, '').replace(/]*>(.*?)</script>/i, '').replace(/]*>(.*?)</noscript>/i, '')
                                                                //we've run the regex to get standard json, now parse it
                                var jsonObject = jQuery.parseJSON(data)
                                cache[ request.term ] = jsonObject;
                                                                response( jsonObject );
                            }                        });                    }
                });
```

 









