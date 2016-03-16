---
layout: post
title: Java- configure apache XML-RPC
---

Communication with an XML-RPC server via Java is extremely easy with the
apache XML-RPC library using the following snippet:








    XmlRpcClient client = new XmlRpcClient();
    XmlRpcClientConfigImpl config = new XmlRpcClientConfigImpl();// Setting timeouts for xmlrpc calls made using XmlRpcSunHttpTransportFactory, the default connection factory 
    int xmlrpcConnTimeout = 10000; // Connection timeout
    int xmlrpcReplyTimeOut = 60000; // Reply timeout
    XmlRpcClientConfigImpl config = new XmlRpcClientConfigImpl();
    config.setServerURL(new URL(serverURL));
    config.setConnectionTimeout(xmlrpcConnTimeout);
    config.setReplyTimeout(xmlrpcReplyTimeOut);
    client.setConfig(config);

### Executing a command

Executing a command is also very simple, build up an array of Object"s
and pass it into the server along with the string command.










    Object[] params = new Object[]{               Integer.valueOf("1"),               
    String.valueOf("email")             };
    Object result = rpcClient.execute("foo.bar", params);



 









