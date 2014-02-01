---
layout: post
title: "MinutesFromNow"
---

# MinutesFromNow



<h2>Namespace</h2>

 
  

<h2>Summary== Returns a date in the future by minutes  ==Example==DateTime then=3.MinutesFromNow();  ==Unit Test</h2>

 
public void MinutesFromNow_Should_Return_DateTime_AddMinutes_Neg3_For_3() {     var today = DateTime.Now;     var then = 3.MinutesFromNow();      Assert.Equal(then, DateTime.Now.AddMinutes(-3)); }  

<h2>Comments</h2>

 SubSonic 3.0 implements this as an extension on System.Int- 2.x uses a static method on SubSonic.Sugar.Dates.
