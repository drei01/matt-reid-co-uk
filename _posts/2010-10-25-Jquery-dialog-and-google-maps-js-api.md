---
layout: post
title: Jquery dialog and google maps js api
---

While overhauling a customer information system I found myself needing
to display a map of a customers postcode without forcing the user to
leave the page.

Here is the solution I came up with.

``` {.js name="code"}



  var map;
  var geocoder;
  function init() { 
    geocoder = new google.maps.Geocoder(); 
  }

  function showAddress(theaddress,element) {      
      if(!geocoder){
              init();
          }
      geocoder.geocode( { 'address': theaddress}, function(results, status) {
          if (status == google.maps.GeocoderStatus.OK) {
              $('#map&#95;dialog').dialog({
                    width:500,
                    height:500,
                    title:"Map for "+theaddress            
                });

            var myOptions = {
                zoom: 8,
                center: results[0].geometry.location,
                mapTypeId: google.maps.MapTypeId.ROADMAP
            };
            map = new google.maps.Map(document.getElementById("map&#95;canvas"),
                            myOptions);             
            var marker = new google.maps.Marker({
                map: map, 
                position: results[0].geometry.location
            });                                
          } else {
            alert("Google could not find the postcode "+theaddress+" : " + status);
          }
        });
    }
 
<%--placeholder for google map popup src: http://marx-tseng.appspot.com/maps/Map_In_jQuery_Dialog.html --%>

    

```

Note then div within a div, this is important otherwise the map gets
restricted to a small 200 x 200 square. Splitting up the divs allows
jquery to resize one and google to use the other for the map.

 









