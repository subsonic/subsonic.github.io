---
layout: post
title: "SubSonic.Extensions.ToConstraintList"
---

# SubSonic.Extensions.ToConstraintList



<h2>Namespace</h2>

 
  

<h2>Summary== Takes the properties of an object and turns them into SubSonic.Query.Constraint. This can be used to push an object as a specification in a query.  ==Example==Product product=new Product(); product.ProductID=1; var query=new Select().From<Product>(); query.Constraints=product.ToConstraintList();  ==Unit Test</h2>

 
public void ToConstraint_List_Should_Return_3_Constraints_For_TestObject() {     var tester = new TestObject()     {         Test1=1,         Test2="Test",         Test3=DateTime.Now.AddDays(1)     };      var constraints = tester.ToConstraintList();     Assert.Equal(3, constraints.Count);     Assert.Equal(1, constraints[0].ParameterValue);     Assert.Equal("Test1", constraints[0].ParameterName);     Assert.Equal("Test", constraints[1].ParameterValue);     Assert.Equal("Test2", constraints[1].ParameterName);     Assert.True((DateTime)constraints[2].ParameterValue>DateTime.Now);     Assert.Equal("Test3", constraints[2].ParameterName);  }  

<h2>Comments</h2>

 SubSonic 3.0 implements this as an extension on System.String - 2.x uses a static method on SubSonic.Sugar.Files
