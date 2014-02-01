---
layout: post
title: "IsWeekDay"
---

# IsWeekDay



<h2>Namespace</h2>

 
  

<h2>Summary== Checks to see if the date is a week day (Mon - Fri)  ==Example==if(DateTime.Today.IsWeekday()){    GoToWork(); }  ==Unit Test</h2>

 
public void IsWeekDay_Should_BeTrue_For_4_16_09_And_IsWeekend_ShouldBe_False() {     var today = DateTime.Parse("4/16/2009");     Assert.True(today.IsWeekDay());     Assert.False(today.IsWeekEnd()); }  

<h2>Comments</h2>

 SubSonic 3.0 implements this as an extension on System.DateTime - 2.x uses a static method on SubSonic.Sugar.Dates.
