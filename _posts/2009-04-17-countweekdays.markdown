---
layout: post
title: "CountWeekdays"
---

# CountWeekdays



<h2>Namespace</h2>

 
  

<h2>Summary== Counts the number of weekdays between two dates.  ==Example==int weekdays=DateTime.Now.CountWeekdays(DateTime.Now.AddDays(100));  ==Unit Test</h2>

 
public void CountWeekdays_Should_Be_86_When_Comparing_1_1_2001_to_5_1_2001() {     var today = DateTime.Parse("1/1/2001");     var then = DateTime.Parse("5/1/2001");     var diff = today.CountWeekdays(then);     Assert.Equal(86, diff); }  

<h2>Comments</h2>

 SubSonic 3.0 implements this as an extension on System.DateTime - 2.x uses a static method on SubSonic.Sugar.Dates.
