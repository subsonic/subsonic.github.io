---
layout: post
title: "DiffHours"
---

# DiffHours



<h2>Namespace</h2>

 
  

<h2>Summary== returns a double indicating the number of hours between 2 dates (past is negative)  ==Example==var diff=DateTime.Now.DiffHours(DateTime.Now.AddHours(3));  ==Unit Test</h2>

 
public void DiffHours_Should_Return_3_For_DateTimeNow_And_AddHours3() {     var today = DateTime.Now;     var then = DateTime.Now.AddHours(3);     var diff = today.DiffHours(then);     Assert.Equal(-3, diff); }  

<h2>Comments</h2>

 SubSonic 3.0 implements this as an extension on System.DateTime - 2.x uses a static method on SubSonic.Sugar.Dates.
