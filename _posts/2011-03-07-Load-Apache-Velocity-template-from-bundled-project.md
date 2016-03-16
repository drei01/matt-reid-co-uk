---
layout: post
title: Load Apache Velocity template from bundled project
---

I recently found myself needing to embed a velocity template in a
project that was being bundled with the web app that I was developing,
this meant that the template file would only be accessible from inside a
jar file.

I found this blog [Apache Velocity - How to load templates from
jar](http://tech--help.blogspot.com/2010/02/solved-apache-velocity-how-to-load.html)
which detailed the problem nicely.

The solution is to set the Velocities resource loader as the classpath,
giving it access to the bundled classpath.

``` {.js name="code"}
Properties props = new Properties();
props.put("resource.loader", "class");
props.put("class.resource.loader.class", "org.apache.velocity.runtime.resource.loader.ClasspathResourceLoader");
VelocityEngine ve = new VelocityEngine();
ve.init(props);
VelocityEngineUtils.MergeTemplateIntoString(ve, "templates/MyFileTemplate.vm", Encoding.UTF8.WebName, model);
```

Matt

 









