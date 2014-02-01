---
layout: post
title: "IsWholeNumber"
---

# IsWholeNumber



<h2>Namespace</h2>

 
  

<h2>Summary== Determines whether a string is a whole number (positive or negative int)  ==Unit Test==[Fact] public void IsWholeNumber_ShouldReturn_True_For_3() {     Assert.True("3".IsWholeNumber()); }  [Fact] public void IsWholeNumber_ShouldReturn_False_For_Neg3() {     Assert.False("-3".IsWholeNumber()); } [Fact] public void IsWholeNumber_ShouldReturn_False_For_3Point3() {     Assert.False("3.3".IsWholeNumber()); }  ==Comments</h2>

 SubSonic 3.0 implements this as an extension method - 2.x uses a static method on SubSonic.Sugar.Numeric.
