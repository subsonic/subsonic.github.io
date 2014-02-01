---
layout: post
title: "GetFormattedMonthAndDay"
---

# GetFormattedMonthAndDay



<h2>Namespace</h2>

 
  

<h2>Summary== Given a datetime object, returns the formatted month and day, i.e. "April 15th"  ==Example==var output=Post.PublishDate.GetFormattedMonthAndDay();  ==Unit Test</h2>

 
public void GetFormattedMonthAndDay_Should_Be_April_16th_For_ParsedDate() {     var today = DateTime.Parse("4/16/2009");     var result = today.GetFormattedMonthAndDay();     Assert.Equal("April 16th", result); }  

<h2>Comments</h2>

 SubSonic 3.0 implements this as an extension on System.DateTime - 2.x uses a static method on SubSonic.Sugar.Dates.
