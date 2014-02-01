---
layout: post
title: "SubSonic.Extensions.ToList"
---

# SubSonic.Extensions.ToList



<h2>Summary== Creates a typed list from an IDataReader.  ==Namespace</h2>

 
  

<h2>Unit Test==[Fact] public void ToList_Should_Load_76_Products_As_TypedList() {     IList<Product> products = new List<Product>();     var db = new Northwind.DB();     using (var reader = db.Select.From<Product>().ExecuteReader()) {         if (reader.Read())             products = reader.ToList<Product>();     }          Assert.Equal(76,products.Count); }  ==Comments</h2>

 SubSonic 3.0 implements this as an extension on System.String - 2.x uses a static method on SubSonic.Sugar.Files.
