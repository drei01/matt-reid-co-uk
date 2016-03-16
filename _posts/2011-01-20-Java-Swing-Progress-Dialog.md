---
layout: post
title: Java Swing Progress Dialog
---

I recently needed to create a progress dialog in a Java Swing
application.

I came across [this
snippet](http://www.java2s.com/Code/Java/Swing-JFC/Creatingamodalprogressdialog.htm)
which was very helpful. The main gist of this being that jDialog's
**setVisible** method is blocking, hence the need to run it in a
seperate thread:

    Thread t = new Thread(new Runnable() {
      public void run() {
        dlg.setVisible(true);
      }
    });
    t.start();

The final result looks very nice (especially with a nice
[lookandfeel](http://download.oracle.com/javase/tutorial/uiswing/lookandfeel/plaf.html)).

![jDialog progress bar](http://i56.tinypic.com/23tqk34.png)

Matt

 









