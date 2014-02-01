---
layout: post
title: "SecondsFromNow"
---

# SecondsFromNow



<h2>Namespace</h2>

 
  

<h2>Summary== Gets a date in the future by seconds.  ==Example==DateTime then=3.SecondsFromNow();  ==Unit Test</h2>

 
public void SecondsFromNow_Should_Return_DateTime_AddSeconds3_For_3() {     var today = DateTime.Now;     var then = 3.SecondsFromNow();      Assert.Equal(then, DateTime.Now.AddSeconds(3)); }  

<h2>Comments</h2>

 SubSonic 3.0 implements this as an extension on System.DateTime - 2.x uses a static method on SubSonic.Sugar.Dates.
