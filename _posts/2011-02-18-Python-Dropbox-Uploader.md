---
layout: post
title: Python Dropbox Uploader
---

For my latest CodeFish project, I needed to be able to upload files to
dropbox from my [SheevaPlug](http://en.wikipedia.org/wiki/SheevaPlug).

This gave me the perfect opportunity to try my first bit of Python code.
I found
[PythonDropboxUploader](http://joncraton.org/blog/uploading-dropbox-python)
and decided to fork it on GitHub (my first time using git as well!).

The simple script uses a browser to upload a single file to dropbox. I
did some googling and managed to change this to loop through all the
files in a directory and upload them.

Looping through a directory was as easy as adding:

``` {.js name="code"}
for file in os.listdir(path):
    if os.path.isfile(os.path.join(path, file)):
        print("found "+os.path.basename(file))
```

The result is available at
[![](http://playerstage.sourceforge.net/images/github-logo.png)](http://github.com/drei01/PythonDropboxUploader)

My experience with git and github was a bit more complicated. It took me
a while to get the private [ssh
key](http://help.github.com/msysgit-key-setup/) working with github and
then the process is slightly different from SVN that i am familiar with.

-   Make a change
-   Commit to local repo
-   Push to master repo on github

There is still a whole lot more to git that I haven't even touched on
and I am hoping to update my
[PythonDropboxUploader](github.com/drei01/PythonDropboxUploader---.html)
fork as I add new capabilities to it.

 









