---
layout: post
title: "Linq Batch Query"
---

# Linq Batch Query



<h2>Summary</h2>

 SubSonic's Batch Query executes multiple calls to the database at once, executing pass-through queries as transactions and SELECT statements as 
single command batches. What this means for SELECT statements is that you will get back an IDataReader with multiple result sets for you to iterate over.  

<h2>Selects with a Batch Query</h2>

 When you create your 
", which accepts and IQueryable
. You can use this to "queue up" a Batch query (this is from our Northwind unit tests):  
var _db=Northwind.DB.CreateDB(); var batch = new BatchQuery(_db.DataProvider);  _db.Queue(from p in _db.Products where p.ProductID

<h2>1 select p); _db.Queue(from p in _db.Products where p.ProductID==2 select p); _db.Queue(from p in _db.Products where p.ProductID </h2>

 3 select p);  int results = 0; using (var rdr = _db.ExecuteBatch()) {     if (rdr.Read())         results++;      if (rdr.NextResult())         if (rdr.Read())             results++;     if (rdr.NextResult())         if (rdr.Read())             results++; }  Assert.AreEqual(3, results);  This will create the following SQL: 
SELECT [t0].[CategoryID],  [t0].[Discontinued],  [t0].[ProductID],  [t0].[ProductName],   [t0].[QuantityPerUnit],   [t0].[ReorderLevel],   [t0].[SomeGuid],   [t0].[SupplierID],   [t0].[UnitPrice],   [t0].[UnitsInStock],   [t0].[UnitsOnOrder] FROM [dbo].[Products] AS t0 WHERE ([t0].[ProductID] = @p1);  SELECT [t0].[CategoryID],  [t0].[Discontinued],  [t0].[ProductID],  [t0].[ProductName],   [t0].[QuantityPerUnit],   [t0].[ReorderLevel],   [t0].[SomeGuid],   [t0].[SupplierID],   [t0].[UnitPrice],   [t0].[UnitsInStock],   [t0].[UnitsOnOrder] FROM [dbo].[Products] AS t0 WHERE ([t0].[ProductID] =  @p2);  SELECT [t0].[CategoryID],  [t0].[Discontinued],  [t0].[ProductID],  [t0].[ProductName],  [t0].[QuantityPerUnit],  [t0].[ReorderLevel],  [t0].[SomeGuid],  [t0].[SupplierID],  [t0].[UnitPrice],  [t0].[UnitsInStock],  [t0].[UnitsOnOrder] FROM [dbo].[Products] AS t0 WHERE ([t0].[ProductID] = @p3);   You can combine this to work with our ToList() IDataReader extension thus:  
db.Queue(from p in db.Products where p.CategoryID 

<h2> 5 select p); db.Queue(from p in db.Products where p.CategoryID == 7 select p); db.Queue(from p in db.Products where p.CategoryID == 9 select p);  List<Products> result1 = null; List<Products> result2 = null; List<Products> result3 = null;   using (IDataReader rdr = qry.ExecuteReader()) {  result1 = rdr.ToList<Products>();    if (rdr.NextResult())   result2 = rdr.ToList<Products>();   if (rdr.NextResult())   result3 = rdr.ToList<Products>();  } ===Inserts, Updates, and Deletes</h2>

 There is more on Batch Queries and Inserts/Updates/Deletes on each of these query pages: *
 *
 *

