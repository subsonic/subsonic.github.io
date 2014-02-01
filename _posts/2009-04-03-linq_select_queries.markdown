---
layout: post
title: "Linq Select Queries"
---

# Linq Select Queries



<h2>Summary</h2>

 SubSonic 3.0 uses 
 as the primary option to query a database. You can perform a multitude of queries in this way, including 
, 
, and 
.  

<h2>Limitations</h2>

 Linq is a C# language feature, NOT a database query language. As such we do our best to try and figure out what you want us to do. This won't always work and there will be times with the query is just plain too complex. 
Important: SubSonic is not as complete as Linq to SQL in terms of Linq translation. Hopefully this will change someday - but if you run into a wall, you can always use our 
.  

<h2>Setup</h2>

 In order to run the queries below, you'll need to generate your 
 and 
 by dropping the SubSonic 
 will fire up the templates and generate the stuff you need.  

<h2>Example Code</h2>

 If you don't know what Linq is or how to use it, 
;     var result = from p in _db.Products                  where p.CategoryID 

<h2> categoryID                  select p;      Assert.AreEqual(7, result.Count()); }  [TestMethod] public void Select_Simple_With_Variable_And_Join() {     int categoryID = 5;     //create DB from QuerySurface, aka "DB"     _db = DB.CreateDB();     var result = from p in _db.Products                  join c in _db.Categories on p.CategoryID equals c.CategoryID                  where p.CategoryID == categoryID                  select p;      Assert.AreEqual(7, result.Count()); }  [TestMethod] public void Select_Simple_With_ForeignKeys() {      //create DB from QuerySurface, aka "DB"     _db = DB.CreateDB();     Order o = _db.Orders.Where(x => x.OrderID == 10248)          .SingleOrDefault();     Assert.AreEqual(3, o.OrderDetails.Count());  }  == Joins </h2>

 SubSonic supports most joins, but you should be aware that you can easily break this. Below is an example of a typical join query, and follows closely with that of Linq to Sql:  
[TestMethod] public void Select_Using_Many_To_Many() {     var db = DB.CreateDB();     var query = from e in db.Employees                 join et in db.EmployeeTerritories on e.EmployeeID equals et.EmployeeID                 join t in db.Territories on et.TerritoryID equals t.TerritoryID                 where e.EmployeeID 

<h2> 1                 select e;      int count = query.Count();     Assert.AreEqual(2, count);     Assert.AreEqual("Daviolo", query.ToList()[0].LastName);  }  [TestMethod] public void LINQ_Join_Query_Take1() {     var results = from c in _db.Customers                   from o in _db.Orders                   from od in _db.OrderDetails                   where c.CustomerID == o.CustomerID && o.OrderID </h2>

 od.OrderID                   select new                   {                       CustomerID = c.CustomerID,                       CompanyName = c.CompanyName,                       ShipAddress = o.ShipAddress,                       ShippedDate = o.ShippedDate,                       ProductID = od.ProductID,                       Quantity = od.Quantity                   };      Assert.AreEqual(2155, results.Count());  }  The latter query here, while syntacticly correct, could possibly cause issues for you if we can't tell what equalities to join on (which could happen with many tables). This same query could be written this way, and would be a bit safer:  
/// <summary> /// An other way to write the above query /// </summary> [TestMethod] public void LINQ_Join_Query_Take2() {     var results = from c in _db.Customers                   join o in _db.Orders on c.CustomerID equals o.CustomerID                   join od in _db.OrderDetails on o.OrderID equals od.OrderID                   select new                   {                       CustomerID = c.CustomerID,                       CompanyName = c.CompanyName,                       ShipAddress = o.ShipAddress,                       ShippedDate = o.ShippedDate,                       ProductID = od.ProductID,                       Quantity = od.Quantity                   };      Assert.AreEqual(2155, results.Count()); }  

<h2>Projecting Results</h2>

 In the last query we used the construct "select new", which is an "Anonymous Type" according to C# - this means that we made the type up on the fly and shoved the query results into it. This can be handy for a number of situations - specifically if you're trying to return a simple result set, or if you need to pump the results into another type.  This code snippet shows how you can project the results of a Select query into a new type, called "ProjectedProduct":  
/// <summary> /// Dummy class for testing use /// </summary> public class ProjectedProduct {     public string SKU { get; set; }     public string Name { get; set; } }  [TestMethod] public void LINQ_Query_Projection() {      var db = DB.CreateDB();     var results = from p in db.Products                   select new ProjectedProduct                   {                       SKU=p.ProductID.ToString(),                       Name=p.ProductName.ToString()                   };     Assert.AreEqual(77, results.Count()); }  

<h2>Failing Query Example</h2>

 
This has limitations. In our testing we've found that if more than one type is involved in this projection (using 
let statements with a child collection for example) - it will fail. This is a known issue!  For example, if we were to use this as our projection test: 
/// <summary> /// Dummy class for testing use /// </summary> public class ProjectedProduct {     public string SKU { get; set; }     public string Name { get; set; }     public IQueryable<ProjectedCategory> Categories { get; set; } } public class ProjectedCategory {     public string Name { get; set; } } IQueryable<ProjectedCategory> GetCategories() {     var db = DB.CreateDB();     return from c in db.Categories            select new ProjectedCategory            {                Name=c.CategoryName                            }; }  [TestMethod] public void LINQ_Query_Projection() {      var db = DB.CreateDB();     var results = from p in db.Products                   let c=GetCategories()                   select new ProjectedProduct                   {                       SKU=p.ProductID.ToString(),                       Name=p.ProductName.ToString(),                       Categories=GetCategories()                   };     Assert.AreEqual(77, results.Count()); }  
FAIL
