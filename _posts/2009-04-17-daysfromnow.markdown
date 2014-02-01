---
layout: post
title: "DaysFromNow"
---

# DaysFromNow



<h2>Namespace</h2>

 
  

<h2>Summary== Returns a date in the future by days.  ==Example==DateTime then=3.DaysFromNow();  ==Unit Test</h2>

 
public void DaysFromNow_Shoud_Return_DateTime_AddDays3_For_3() {             var today = DateTime.Now;             var then = 3.DaysFromNow();              Assert.Equal(then, DateTime.Now.AddDays(3));         }  

<h2>Comments</h2>

 SubSonic 3.0 implements this as an extension on System.Int- 2.x uses a static method on SubSonic.Sugar.Dates.
