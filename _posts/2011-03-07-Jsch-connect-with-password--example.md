---
layout: post
title: Jsch connect with password- example
---

I am working on my latest codefish android app which utilises
[Jsch](http://www.jcraft.com/jsch/) to send files over SFTP. I couldn't
find a complete example of creating an SFTP connection using a password
so I thought I'd post one.

Here is the code:

``` {.js name="code"}
import java.io.File;
import java.util.Properties;
import java.util.Vector;

import com.jcraft.jsch.ChannelSftp;
import com.jcraft.jsch.ChannelSftp.LsEntry;
import com.jcraft.jsch.JSch;
import com.jcraft.jsch.Session;

public class ConnectWithPass {

    public static void main(String[] args) throws Exception {
        
        if (args.length < 3) {
            throw new Exception("not enough arguments");
        }
        
        String serverUrl = args[0];
        String userName = args[1];
        String password = args[2];
        
        JSch jsch = new JSch();
        
        Properties config = new Properties();
        config.put("StrictHostKeyChecking", "no");
        config.put("compression.s2c", "zlib,none");
        config.put("compression.c2s", "zlib,none");
        
        Session session = jsch.getSession(userName, serverUrl);
        session.setConfig(config);
        session.setPort(22);
        session.setPassword(password);
        session.connect();
        
        ChannelSftp channel = (ChannelSftp) session.openChannel("sftp");
        channel.connect();

        @SuppressWarnings("unchecked")
        final Vector files = channel.ls(".");
        for (LsEntry obj : files) {
            System.out.println(obj.toString());
        }   
        
        channel.disconnect();
        session.disconnect();
    }

}
```

The code creates a connection with a password and then performs an *ls*
command to list all the files in the server's base directory.

Thanks to my workmate @carlbunting for help with the code.

*note: **jsch.jar** and **jzlib.jar** are the required libraries to get
this example to work*

Matt

 









