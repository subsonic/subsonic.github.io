---
layout: post
title: "CountWeekends"
---

# CountWeekends



<h2>Namespace</h2>

 
  

<h2>Summary== Counts the number of weekends between two dates.  ==Example==int days=DateTime.Now.CountWeekends(DateTime.Now.AddDays(100));  ==Unit Test</h2>

 
public void CountWeekends_Should_Be_86_When_Comparing_1_1_2001_to_5_1_2001() {     var today = DateTime.Parse("1/1/2001");     var then = DateTime.Parse("5/1/2001");     var diff = today.CountWeekends(then);     Assert.Equal(34, diff); }  

<h2>Comments</h2>

 SubSonic 3.0 implements this as an extension on System.DateTime - 2.x uses a static method on SubSonic.Sugar.Dates.
