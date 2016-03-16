---
layout: post
title: JQuery Floating Menu Bar
---

So you have a menu bar under your website header, but wouldn"t it be
cool to keep that menu bar at the top of the client's screen even when
they scroll out of view?

Here's how I solved that problem.

First I have my webpage header, it has a logo at the top and the menu
bar in a UL underneath.

``` {.js name="code"}
    
        
                        
" class="_logo" alt="test"/>                         
CRM: ${client.name} (${client.customerNumber}/${client.branchNumber})            
" class="user_icon"/><%=request.getRemoteUser()%>        
                      
            
" id="menu_cisHome" >CRM Home            
Quick Search            
Reports            
"  class='selected">All Tasks
"  
class='selected">All Open Tasks            
" class='selected">My Open Tasks            
" class='selected">All My Tasks            
" class='selected">All Unassigned Tasks                           
">Logout                                     
                                    
              
