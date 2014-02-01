---
layout: post
title: "Active Record Fluent Query"
---

# Active Record Fluent Query

= ActiveRecord Fluent Query Examples  =  If you're using the ActiveRecord templates then as well SubSonic's Linq implementation you can also make use of Fluent Queries  All of the samples below assume the Northwind database.  

<h2> Simple Select with string columns ==int records = new NorthwindDB.SelectColumns(new string[] { "productID"})   .From<Product>().GetRecordCount();  Assert.IsTrue(records == 77); == Simple Select with typed columns </h2>

 
int records = new NorthwindDB.Select(     new string[] {       ProductTable.ProductIDColumn,        Product.ProductNameColumn })   .From<Product>().GetRecordCount();  Assert.IsTrue(records 

<h2> 77);  == Returning a Single object </h2>

 
Product p = new NorthwindDB.Select   .From<Product>()   .Where(ProductTableProduct.IDColumn).IsEqualTo(1)   .ExecuteSingle<Product>();  Assert.IsNotNull(p); 

<h2> Returning all columns </h2>

 
int records = new NorthwindDB.Select   .From<Product>().GetRecordCount();  Assert.IsTrue(records 

<h2> 77); == Simple Where </h2>

 
int records = new NorthwindDB.Select   .From<Product>()   .Where(ProductTable.CategoryIDColumn).IsEqualTo(5)   .GetRecordCount();  Assert.AreEqual(7, records); 

<h2> Simple Where with And (as List) </h2>

 
List<Product> products = new NorthwindDB.Select   .From<Product>()   .Where(ProductTable.CategoryIDColumn).IsEqualTo(5)   .And(ProductTable.ProductIDColumn).IsGreaterThan(50)   .ExecuteTypedList<Product>(); 

<h2> Simple Inner Join </h2>

 
SubSonic.SqlQuery query = NorthwindDB.Select   .From<OrderDetail>()   .InnerJoin<Product>()   .Where(ProductTable.CategoryIdColumn).IsEqualTo(5); 

<h2> Multiple Joins As List </h2>

 
List<Customer> customersByCategory = new NorthwindDB.Select   .From<Customer>()   .InnerJoin<Order>()   .InnerJoin<OrderDetail>(OrderDetailTable.OrderIDColumn, OrderTable.OrderIDColumn)   .InnerJoin<Product>(ProductTable.ProductIDColumn, OrderDetailTable.ProductIDColumn)   .Where(ProductTable.CategoryIDColumn).IsEqualTo(5)   .ExecuteTypedList<Customer>(); 

<h2> Left Outer Join With Generics </h2>

 
SubSonic.SqlQuery query = new NorthwindDB.Select   .From<Customer>()   .LeftOuterJoin<Order>();   query.Aggregates  = new List<Aggregate> {      new Aggregate(CustomerTable.CustomerNameColumn, AggregateFunction.GroupBy) }; 

<h2> Simple Select With Collection Result </h2>

 
List<Product> products = new NorthwindDB.Select   .From<Product>()   .ExecuteTypedList<Product>(); 

<h2> Simple Select With LIKE </h2>

 
List<Product> products = new NorthwindDB.Select   .From<Product>()   .InnerJoin<Category>()   .Where(CategoryTable.CategoryNameColumn).Like("c%")   .ExecuteTypedList<Product>(); 

<h2> Using Nested Where/And/Or </h2>

 
List<Product> products = new NorthwindDB.Select   .From<Product>()   .WhereExpression(ProductTable.CategoryIDColumn).IsEqualTo(5)   .And(ProductTable.ProductIdColumn).IsGreaterThan(10)   .OrExpression(ProductTable.CategoryIdColumn).IsEqualTo(2)   .And(ProductTable.ProductIdColumn).IsBetweenAnd(2, 5)   .ExecuteTypedList<Product>();  List<ProductCollection> products = new NorthwindDB.Select   .From<Product>()   .WhereExpression(ProductTable.CategoryIDColumn).IsEqualTo(5)     .And(ProductTable.ProductIdColumn).IsGreaterThan(10)     .Or(ProductTable.CategoryIDColumn).IsEqualTo(2)   .AndExpression(ProductTable.ProductIdColumn).IsBetweenAnd(2, 5)   .ExecuteTypedList<Product>(); 

<h2> Simple Paged Query </h2>

 
SubSonic.SqlQuery query = new NorthwindDB.Select   .From<Product>()   .Paged(1, 20)   .Where(ProductTable.ProductIdColumn).IsLessThan(100); 

<h2> Paged Query With Join </h2>

 
SubSonic.SqlQuery query = new NorthwindDB.SelectColumns(new string[] {        "ProductId",        "ProductName",        "CategoryName" })   .From<Product>()   .InnerJoin<Category>()   .Paged(1, 20); Simple IN Query 
int records = new NorthwindDB.Select()   .From<Product>()   .Where(ProductTable.ProductIdColumn).In(1, 2, 3, 4, 5)   .GetRecordCount();  Assert.IsTrue(records 

<h2> 5); == Using IN With Nested Select </h2>

 
int records = new NorthwindDB.Select.From<Product>()   .Where(ProductTable.ProductIdColumn)   .In(     new NorthwindDB.SelectColumns(ProductTable.ProductIdColumn)       .From<Product>()       .Where(ProductTable.CategoryIdColumn).IsEqualTo(5))   .GetRecordCount(); 

<h2> Using Multiple INs </h2>

 
SubSonic.SqlQuery query = new NorthwindDB.Select   .From<Product>()   .Where(Product.CategoryIDColumn).In(2, 4)   .And(Product.SupplierIDColumn).In(3, 9);
