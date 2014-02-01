---
layout: post
title: "HoursFromNow"
---

# HoursFromNow



<h2>Namespace</h2>

 
  

<h2>Summary== Loads the text from the specified file as a string  ==Example==DateTime then=3.HoursFromNow();  ==Unit Test</h2>

 
public void HoursFromNow_Shoud_Return_DateTime_AddHours3_For_3() {             var today = DateTime.Now;             var then = 3.HoursFromNow();              Assert.Equal(then, DateTime.Now.AddHours(3));         }  

<h2>Comments</h2>

 SubSonic 3.0 implements this as an extension on System.Int- 2.x uses a static method on SubSonic.Sugar.Dates.
