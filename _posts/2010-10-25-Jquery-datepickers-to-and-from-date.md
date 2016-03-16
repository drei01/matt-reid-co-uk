---
layout: post
title: Jquery datepickers to and from date
---

I was recently using 2 date pickers to allow the user to select a date
range and was in need of a dynamic date-restriction function. Here it
is:

``` {.js name="code"}
$('.datePicker').datepicker({
                dateFormat:"dd-mm-yy",
                showAnim:"show",
                beforeShow: customRange
            });

    <%-- the toDate can only select dates after the fromDate (and vice-versa) --%>
    function customRange(a) {
        var b = new Date();             
        var c = new Date();
        c.setFullYear(0001, 01, 01);
        if ($(a).hasClass('toDate')) {
            d = $('.fromDate').datepicker('getDate');  
            if ( d != null) {
                c = d;                  
            }                                   
        }
        else if($(a).hasClass('fromDate')){
            d = $('.toDate').datepicker('getDate');
            if ( d != null) {
                c = d;                  
            }
            return {
                maxDate: c
            }   
        }
        return {
            minDate: c,
            maxDate: b
        }
    }
```

and the html:

``` {.js name="code"}
 
```

 









