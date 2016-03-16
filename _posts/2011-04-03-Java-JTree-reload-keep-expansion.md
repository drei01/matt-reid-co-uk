---
layout: post
title: Java JTree reload keep expansion
---

Just a quick post today. I was having problems refreshing a JTree and
keeping the expanded paths in-tact. Instead of calling **reload()** on
the[model](http://download.oracle.com/javase/6/docs/api/javax/swing/tree/TreeModel.html) i
needed to be calling
[nodeChanged](http://download.oracle.com/javase/6/docs/api/javax/swing/tree/DefaultTreeModel.html#nodesChanged(javax.swing.tree.TreeNode,%20int%5B%5D)) **even
if a node is being removed**. Here is the snippet:










    ((DefaultTreeModel)tree.getModel()).nodeChanged(actualNode);//notify the model that the node has changed

Matt

 









