---
layout: post
title: "DiffMinutes"
---

# DiffMinutes



<h2>Namespace</h2>

 
  

<h2>Summary== Returns a double which indicates the difference in minutes between to dates (past is negative)  ==Example==var minutes=DateTime.Now.DiffMinutes(DateTime.Now.AddMinutes(3));  ==Unit Test</h2>

 
[Fact] public void DiffMinutes_Should_Return_3_For_DateTimeNow_And_AddMinutes3() {     var today = DateTime.Now;     var then = DateTime.Now.AddMinutes(3);     var diff = today.DiffMinutes(then);     Assert.Equal(-3, diff); }  

<h2>Comments</h2>

 SubSonic 3.0 implements this as an extension on System.DateTime - 2.x uses a static method on SubSonic.Sugar.Dates.
