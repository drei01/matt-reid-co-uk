---
layout: post
title: Market requires versionCode to be set to a positive 32-bit integer
---

When uploading my app to the Android Market, I got the following error.

> Market requires versionCode to be set to a positive 32-bit integer in
> AndroidManifest.xml

To solve this, I needed to put a uses-sdk tag in my manifest.xml like:

``` {.js name="code"}

```

Check
[here](http://developer.android.com/guide/appendix/api-levels.html) for
the version number to use.

You must also have a package, version number and version code in your
main manifest tag:

``` {.js name="code"}

```

The version code should be updated each time you deploy the app (i.e
major version) and the version name can be the specific version of your
app (i.e minor version)

**Note** the package must be unique within the market or you will not be
alllowed to upload the app.

Enjoy

Matt

 









