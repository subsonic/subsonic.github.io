---
layout: post
title: "Linq Aggregate Queries"
---

# Linq Aggregate Queries



<h2>Summary== You can run aggregate queries using our Linq engine in the exact same way you do with Linq to Sql:[TestMethod]         public void Aggregates_Should_Run_Count_Old_Skool() {              decimal result = (decimal)_db.Products                     .Count();              Assert.IsTrue(result > 0);          }         [TestMethod]         public void Aggregates_Should_Run_Avg_Old_Skool() {              decimal result = (decimal)_db.Products                     .Average(x=>x.ProductID);              Assert.IsTrue(result > 0);          }          [TestMethod]         public void Aggregates_Should_Run_Sum_Old_Skool() {              decimal result = (decimal)_db.Products                     .Sum(x => x.UnitPrice);              Assert.IsTrue(result > 0);          }  As with all queries, if you try to get to deep into the analytics here you may end up in trouble. These are meant for the basic "80%" scenarios, where you need a sum/average/whatever. Ideally, the aggregate query you're trying to write will give you what you want to know.  ==Rollup Queries</h2>

 In this example we'll rollup a count of Products for each Category in Northwind - and it works just fine: 
[TestMethod] public void Aggregates_Should_Run_Joined_Count_Old_Skool() {      var result = from c in _db.Categories                      select new                      {                          Name = c.CategoryName,                          Count = _db.Products.Where(x => x.CategoryID ==                                        c.CategoryID).Count()                      };      Assert.AreEqual(8,result.Count());     Assert.AreEqual("Beverages", result.ToList()[0].Name);     Assert.AreEqual(12, result.ToList()[0].Count); }  This produces this SQL here:  
SELECT [t0].[CategoryName], (   SELECT COUNT(*)   FROM [dbo].[Products] AS t1   WHERE ([t1].[CategoryID] = [t0].[CategoryID])   ) AS c0 FROM [dbo].[Categories] AS t0  But do you see a weirdness in there on how the results could fail (aside from the fact that I'm hitting the live DB)? I'm not specifying an ORDER BY and therefore the Assert could fail if, for some reason, "Beverages" wasn't the first record (which could easily happen if we switched indexing around).  

<h2>Failing Aggregate Query</h2>

 I could alter the query to this:  
var result = from c in _db.Categories                  orderby c.CategoryID                  select new                  {                      Name = c.CategoryName,                      Count = _db.Products.Where(x => x.CategoryID                           == c.CategoryID).Count()                  };  ... which would produce this SQL:  
SELECT [t0].[CategoryName], (   SELECT COUNT(*)   FROM [dbo].[Products] AS t1   WHERE ([t1].[CategoryID] = [t0].[CategoryID])   ) AS c0 FROM [dbo].[Categories] AS t0 ORDER BY [t0].[CategoryID]  ... and boom, we have an issue. "CategoryID" is not included in the SELECT statement, so we have a problem and we get an error. Even if I include "CategoryID" in the projection, it still won't work. 
This is a limitation of our parser and we're working on a fix.  The point is - there are limitations (and yes, some of them are silly) and we're trying to get those fixed up. If you do run into a situation like this, you can always use our 
 to get around it.  

<h2>Using The Query Surface Aggregates</h2>

 The 
 - aka the "Data Context" defines aggregate queries for you straight away, and you can use them as "quickie" aggregate calls to the DB:  
[TestMethod] public void Aggregates_Should_Return_Average() {      decimal result = (decimal)_db.Avg<Product>(x => x.UnitPrice).ExecuteScalar();     Assert.IsTrue(result > 0);  }  [TestMethod] public void Aggregates_Should_Return_Max() {     var result1 = (int)_db.Max<Product>(x => x.ProductID).ExecuteScalar();     Assert.AreEqual(result1, 77);      var result2 = _db.Products.Max(x => x.ProductID);     Assert.AreEqual(result1, result2);  }  [TestMethod] public void Aggregates_Should_Return_Min() {     var result1 = (int)_db.Min<Product>(x => x.ProductID).ExecuteScalar();     Assert.AreEqual(result1, 1);      var result2 = _db.Products.Min(x => x.ProductID);     Assert.AreEqual(result1, result2); }
