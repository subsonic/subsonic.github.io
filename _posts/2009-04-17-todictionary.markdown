---
layout: post
title: "ToDictionary"
---

# ToDictionary



<h2>Namespace</h2>

 
  

<h2>Summary== Sends the properties/values of an object to a Dictionary<string,object></string,object>.  ==Example==Dictionary&lt;string,object&gt; objectValues=myObject.ToDictionary(); ==Unit Test</h2>

 
public void ToDictionary_Should_Return_5_Items_For_Test_Object() {     var tester = new     {         thing1 = "test",         thing2 = DateTime.Now,         thing3 = 1,         thing4 = 2.03M,         thing5 = Guid.NewGuid()     };      var result = tester.ToDictionary();     Assert.Equal(5, result.Count); }  

<h2>Comments</h2>

 SubSonic 3.0 implements this as an extension method - 2.x uses a static method on SubSonic.Sugar.Numeric.
