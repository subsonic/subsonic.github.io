---
layout: post
title: "SecondsAgo"
---

# SecondsAgo



<h2>Namespace</h2>

 
  

<h2>Summary== Gets a date in the past according to seconds  ==Example==DateTime then=3.SecondsAgo();  ==Unit Test</h2>

 
public void SecondsAgo_Should_Return_DateTime_AddSeconds_Neg3_For_3() {     var today = DateTime.Now;     var then = 3.SecondsAgo();      Assert.Equal(then, DateTime.Now.AddSeconds(-3)); }  

<h2>Comments</h2>

 SubSonic 3.0 implements this as an extension on System.Int - 2.x uses a static method on SubSonic.Sugar.Dates.
