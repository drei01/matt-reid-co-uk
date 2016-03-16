---
layout: post
title: Android writing to file
---

If you want to write a file specific to your application (I am using
this for object persistence) then here is a simple tutorial for reading
and writing files without getting the dreaded

> read only filesystem

exception.

Writing a file (i am using on object writer but you can use any writer)

``` {.js name="code"}
FileOutputStream f_out = c.openFileOutput(filename, Context.MODE_PRIVATE);

        ObjectOutputStream obj_out = new ObjectOutputStream(f_out);

        obj_out.writeObject(f);
```

Reading a file

``` {.js name="code"}
// Read from disk using FileInputStream.
        FileInputStream f_in = c.openFileInput(filename);

        // Read object using ObjectInputStream.
        ObjectInputStream obj_in = new ObjectInputStream(f_in);

        // Read an object.
        Object obj = obj_in.readObject();

        // Is the object that you read in, say, an instance
        // of the Vector class?
        if (obj instanceof ArrayList) {
            return (ArrayList) obj;

        }
```

 









