---
layout: post
title: Hibernate criteria count rows
---

Just a quick one that I forgot to note down. If you want to count rows
using a hibernate query, here is the bit of magic that you need.








    return (Number) session.createCriteria(Bananas.class).setProjection(Projections.rowCount()).uniqueResult();



 









