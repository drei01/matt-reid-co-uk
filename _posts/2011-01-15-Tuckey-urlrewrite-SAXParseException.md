---
layout: post
title: Tuckey urlrewrite SAXParseException
---

I have been using the very good [Tuckey
urlrewrite](http://www.tuckey.org/urlrewrite/) filter on J2EE website
recently and came across the following error for one of my filters.

``` {.js name="code"}
org.xml.sax.SAXParseException: The reference to entity "documentNumber" must end with the ';' delimiter.

      at com.sun.org.apache.xerces.internal.parsers.DOMParser.parse(DOMParser.java:264)

      at com.sun.org.apache.xerces.internal.jaxp.DocumentBuilderImpl.parse(DocumentBuilderImpl.java:292)

      at javax.xml.parsers.DocumentBuilder.parse(DocumentBuilder.java:123)

      at org.tuckey.web.filters.urlrewrite.Conf.loadDom(Conf.java:208)

      at org.tuckey.web.filters.urlrewrite.Conf.(Conf.java:130)
```

This exception perplexed me for a while and it took a bit of googling to
find the answer as the exception lead me in the wrong direction.

Because the url filters are written in XML, they cannot contain the
**&** character in plaintext. The answer to this annoying exception is
to:

*replace all* **&** *characters with* **&**

i.e:

``` {.js name="code"}

           /test.php?foo=bar&baz=(.*)
           /testing/$1

```

becomes

``` {.js name="code"}

           /test.php?foo=bar&baz=(.*)
           /testing/$1

```

I hope this helps anyone who comes across the same problem.

 









