---
layout: post
title: "ReadableDiff"
---

# ReadableDiff



<h2>Namespace</h2>

 
  

<h2>Summary== Displays the difference in time between the two dates. Return example is "12 years 4 months 24 days 8 hours 33 minutes 5 seconds  ==Example==string diff=DateTime.Now.ReadableDiff(DateTime.Now.AddYears(3));  ==Unit Test</h2>

 
public void ReadableDiff_Should_Say_3_Years_Ago_When_DateTimeNow_Is_Diffed_With_DateTimeNow_AddYears_3() {     var today = DateTime.Now;     var then = DateTime.Now.AddYears(3);     var diff = today.ReadableDiff(then);     Assert.Equal("3 years ago", diff); }  

<h2>Comments</h2>

 SubSonic 3.0 implements this as an extension on System.DateTime - 2.x uses a static method on SubSonic.Sugar.Dates.
