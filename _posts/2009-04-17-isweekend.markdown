---
layout: post
title: "IsWeekend"
---

# IsWeekend



<h2>Namespace</h2>

 
  

<h2>Summary== Checks to see if the date is Saturday or Sunday  ==Example==if(DateTime.Today.IsWeekend()){    PartyLikeARockStar(); }  ==Unit Test</h2>

 
public void IsWeekEnd_Should_BeTrue_For_4_18_09_And_IsWeekDay_ShouldBe_False() {     var today = DateTime.Parse("4/18/2009");     Assert.False(today.IsWeekDay());     Assert.True(today.IsWeekEnd()); }  

<h2>Comments</h2>

 SubSonic 3.0 implements this as an extension on System.DateTime - 2.x uses a static method on SubSonic.Sugar.Dates.
