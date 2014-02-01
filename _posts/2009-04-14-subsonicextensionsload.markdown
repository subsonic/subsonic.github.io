---
layout: post
title: "SubSonic.Extensions.Load"
---

# SubSonic.Extensions.Load



<h2>Summary== Coerces an IDataReader to try and load an object using name/property matching  ==Namespace</h2>

 
  

<h2>Unit Test==public void Load_Should_Load_New_Product() {     Product p = new Product();     var db = new Northwind.DB();     using (var reader = db.Select.From<Product>()         .Where("ProductID").IsEqualTo(1).ExecuteReader()) {         if (reader.Read())             reader.Load(p);     }      Assert.Equal(p.ProductID, 1); }  ==Comments</h2>

 SubSonic 3.0 implements this as an extension on System.String - 2.x uses a static method on SubSonic.Sugar.Files.
