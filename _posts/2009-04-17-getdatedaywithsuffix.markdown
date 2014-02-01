---
layout: post
title: "GetDateDayWithSuffix"
---

# GetDateDayWithSuffix



<h2>Namespace</h2>

 
   

<h2>Summary== Given a datetime object, returns the formatted day, "15th"  ==Example==var output="The post was published on the "+Post.PublishedDate.GetDateDayWithSuffix();  ==Unit Test</h2>

 
public void GetDateDayWithSuffix_Should_Be_April_16th_For_ParsedDate() {     var today = DateTime.Parse("4/16/2009");     var result = today.GetDateDayWithSuffix();     Assert.Equal("16th", result); }  

<h2>Comments</h2>

 SubSonic 3.0 implements this as an extension on System.DateTime - 2.x uses a static method on SubSonic.Sugar.Dates.
