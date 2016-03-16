---
layout: post
title: Spring Social M3 Example
---

I couldn't find a simple, complete example of a spring social
application online so I decided to post my own. The resulting app is
available on [google
code](http://code.google.com/p/springsocialm3example/) and is an example
of authenticating a user with Facebook, although a similar approach is
applied to Twitter/Linkedin etc.

Configuration
=============

The app is a standard Spring Web MVC project but some additional
configuration is needed to create the beans for interacting with
Facebook.

         
        
        
        
        
        
            
        
        
            
            
           
        

The FacebookWebArgumentResolver is the bean that handles the facebook
cookie that gets created when a user authenticates with Facebook.

The View
========

Setting up javascript authentication with Facebook is very easy using
spring social. A tag is provided that does all of the hard work for you.
This means that there is no contact with the server for the
authentication (the js communicates directly with Facebook which then
stores a cookie on the client).

            
                
                
                    
                Connect to Facebook
            
            
            
            

The Controller
==============

Once the cookie is stored on the client then when they make a request to
a page that requires authentication, spring can check the credentials
against the facebook cookie.

        @RequestMapping(value="auth.do")
        public ModelAndView authenticate(@FacebookCookieValue(required=false, value="access_token") String cookie){
            if(cookie == null){
                return new ModelAndView("authfail");
            }
            
            FacebookApi facebook = new FacebookTemplate(cookie);
            

 









