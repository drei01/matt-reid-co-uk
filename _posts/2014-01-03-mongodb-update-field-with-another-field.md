---
layout: post
title: mongodb update field with another field
---

Using a standard relation database it is easy to update the value of a
column with that of another using a simple update statement. This is not
the case with mongodb, luckily you can perform a simple query to produce
the same result. By looping through every matching element in a
collection and then creating an update for that object we can obtain the
same result (all be it in a rather more elaborate manner).








    db.person.find().forEach(
        function (elem) {
          elem.name = elem.firstname + ' '+ elem.lastname;

          // don't forget to save the updated document
          db.person.save(elem);
        }
      )



 









