---
layout: post
title: java.lang.VerifyError- class net.sf.cglib.core.DebuggingClassWriter
---

A note to anyone getting the
following message *java.lang.VerifyError: class
net.sf.cglib.core.DebuggingClassWriter overrides final method visit *








The problem is a mismatch in the versions of asm and cglib in your
webapp. cglib 2.2 pulls in asm version 3.1 (there should not be a higher
version in your classpath)










                cglib            cglib          2.2          compile      



 









