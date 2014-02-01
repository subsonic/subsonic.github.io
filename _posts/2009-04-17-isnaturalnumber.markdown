---
layout: post
title: "IsNaturalNumber"
---

# IsNaturalNumber



<h2>Namespace</h2>

 
  

<h2>Summary== Verifies if a string is a natural number  ==Unit Test==[Fact] public void IsNatural_ShouldReturn_True_For_3() {     Assert.True("3".IsNaturalNumber()); }  [Fact] public void IsNatural_ShouldReturn_False_For_Neg3() {     Assert.False("-3".IsNaturalNumber()); } [Fact] public void IsNatural_ShouldReturn_False_For_3Point3() {     Assert.False("3.3".IsNaturalNumber()); }  ==Comments</h2>

 SubSonic 3.0 implements this as an extension method - 2.x uses a static method on SubSonic.Sugar.Numeric.
