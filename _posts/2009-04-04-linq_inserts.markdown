---
layout: post
title: "Linq Inserts"
---

# Linq Inserts



<h2>Summary</h2>

 You can use the goodness that is the Linq syntax to insert data into your database. It's important to note that SubSonic IS NOT AN ORM - it's a query tool (subtle difference) and therefore it doesn't do object tracking. There's nothing stopping you from creating a 
. This is fine and dandy if you like working that way - but we think this is a Big Lie.   The web is a stateless medium - this sort of "contextual tracking" is just not the Real World and we don't drink that beer.  

<h2>Setup</h2>

 Make sure you 
 SubSonic by adding a reference, setting up your DB connection, and then adding the templates to your project.  

<h2>Simple Inserts</h2>

 You can perform inserts very simply by using the 
;  This will execute an INSERT statement thus: 
INSERT INTO   

<h2>Using the Repository</h2>

 Many people don't want to write this stuff by hand and would rather use objects. You can definitely do this by using our 
, which is generated for you if you using our default T4 templates.  

<h2>=Simple Insert=</h2>

 This will add a Product to the Products table (using Northwind) 
var repo=new NorthwindRepository<Product>();  var p = new Product(); p.ProductName = "Test"; p.UnitPrice = 100; //...// repo.Add(p);  

<h2>=Multiple Inserts=</h2>

 You can also insert an IEnumerable collection of items to the Repository, and they will be saved in a transaction:  
var repo=new NorthwindRepository<Product>(); List<Product> queue = new List<Product>(); for (int i = 1; i < 100; i++) {     var p = new Product();     p.ProductName = "Test";     p.UnitPrice = 100;     queue.Add(p); } repo.Add(queue);  This latter example uses SubSonic's 
 to execute multiple items at once inside a transaction.
