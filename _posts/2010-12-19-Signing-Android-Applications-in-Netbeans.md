---
layout: post
title: Signing Android Applications in Netbeans
---

I am using the netbeans android plugin for app development. I finally
came to submit my app but had a lot of trouble with a *ZipException*
when trying to digitally sign the application.

After a lot of googling, here's how to solve the problem.

-   Switch to **file** view in netbeans and find *build.xml* (it should
    be empty)

![netbeans android build](http://i54.tinypic.com/331fwnb.jpg)

-   Add the following to the file

    ``` {.js name="code"}
            
                
                
                
                
            
            
        
         
    ```

-   **Right click** on build.xml and select *run target* ->
    *unsigned*

You know have an unsigned version (***-unsigned.apk) of your app ready
to be signed as in this post: [Signing your android
app](%22http-/bees4honey.com/blog/tutorial/how-to-prepare-android-application-for-market/.html)

 









