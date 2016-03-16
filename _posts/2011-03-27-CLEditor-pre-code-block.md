---
layout: post
title: CLEditor pre code block
---

I have changed my post editor to use
[CLEditor](http://premiumsoftware.net/cleditor/)rather than WMeditor
which had some problems when editing a post. One feature which is
obviosuly really important to me is to be able to include code in
*pre* blocks. Luckily I found [this
plugin](https://gist.github.com/837281) at github which makes it easy to
include this feature in the editor.


















Once this code has been included in a *script* tag then it is easy to
add to the editor by calling.










    $('#myTextarea').cleditor({
        controls:     // controls to add to the toolbar
        "bold italic underline strikethrough subscript superscript | font size " +
        "style | color highlight removeformat | bullets numbering | outdent " +
        "indent | alignleft center alignright justify | undo redo | " +
        "rule image link unlink | cut copy paste pastetext | print source | pastecode"
        });



 









