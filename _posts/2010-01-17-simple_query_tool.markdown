---
layout: post
title: "Simple Query Tool"
---

# Simple Query Tool

SubSonic comes with a variety of ways to talk to your database. Originally we had a query tool that was a little verbose and somewhat difficult to use. That has since been refined to use a "fluent interface" - which is the chaining of methods to be, essentially, human-readable.  These examples are specific to SubSonic 2 see 
;  Simple Select with typed columns 
int records = new Select(Product.ProductIDColumn, Product.ProductNameColumn).                 From<Product>().GetRecordCount();             Assert.IsTrue(records == 77);   Returning a Single object 
Product p = new Select().From<Product>().                Where("ProductID").IsEqualTo(1).ExecuteSingle<Product>();             Assert.IsNotNull(p); Returning a Single object using generated strongly typed variables 
Product p = new Select().From<Product>().                Where(Product.Columns.ProductID).IsEqualTo(1).ExecuteSingle<Product>();             Assert.IsNotNull(p);  Returning all columns 
int records = new Select().From("Products").GetRecordCount();             Assert.IsTrue(records == 77); Simple Where 
int records = new Select().From("Products").                 Where("categoryID").IsEqualTo(5).GetRecordCount();             Assert.AreEqual(7, records);  Simple Where with And (as Collection) 
ProductCollection products =                 DB.Select().From("Products")                     .Where("categoryID").IsEqualTo(5)                     .And("productid").IsGreaterThan(50)                     .ExecuteAsCollection<ProductCollection>(); Simple Inner Join 
SubSonic.SqlQuery q = new Select("productid").From(OrderDetail.Schema)                 .InnerJoin(Product.Schema)                 .Where("CategoryID").IsEqualTo(5); Simple Join With Table Enum 
SubSonic.SqlQuery q = new Select().From(Tables.OrderDetail)                 .InnerJoin(Tables.Product)                 .Where("CategoryID").IsEqualTo(5); Multiple Joins As Collection 
CustomerCollection customersByCategory = new Select()                 .From(Customer.Schema)                 .InnerJoin(Order.Schema)                 .InnerJoin(OrderDetail.OrderIDColumn, Order.OrderIDColumn)                 .InnerJoin(Product.ProductIDColumn, OrderDetail.ProductIDColumn)                 .Where("CategoryID").IsEqualTo(5)                 .ExecuteAsCollection<CustomerCollection>(); Left Outer Join With Generics 
SubSonic.SqlQuery query = DB.Select(Aggregate.GroupBy("CompanyName"))                 .From<Customer>()                 .LeftOuterJoin<Order>(); Left Outer Join With Schema 
SubSonic.SqlQuery query = DB.Select(Aggregate.GroupBy("CompanyName"))                 .From(Customer.Schema)                 .LeftOuterJoin(Order.CustomerIDColumn, Customer.CustomerIDColumn); Left Outer Join With Magic Strings 
SubSonic.SqlQuery query = DB.Select(Aggregate.GroupBy("CompanyName"))                 .From("Customers")                 .LeftOuterJoin("Orders"); Simple Select With Collection Result 
ProductCollection p = Select.AllColumnsFrom<Product>()                 .ExecuteAsCollection<ProductCollection>(); Simple Select With LIKE 
ProductCollection p = DB.Select()                 .From(Product.Schema)                 .InnerJoin(Category.Schema)                 .Where("CategoryName").Like("c%")                 .ExecuteAsCollection<ProductCollection>(); Using Nested Where/And/Or 
ProductCollection products = Select.AllColumnsFrom<Product>()                 .WhereExpression("categoryID").IsEqualTo(5).And("productid").IsGreaterThan(10)                 .OrExpression("categoryID").IsEqualTo(2).And("productID").IsBetweenAnd(2, 5)                 .ExecuteAsCollection<ProductCollection>();              ProductCollection products = Select.AllColumnsFrom<Product>()                 .WhereExpression("categoryID").IsEqualTo(5).And("productid").IsGreaterThan(10)                 .Or("categoryID").IsEqualTo(2).AndExpression("productID").IsBetweenAnd(2, 5)                 .ExecuteAsCollection<ProductCollection>();   OR when the above is done manually (notice manual opening and closing of expressions):              ProductCollection products = Select.AllColumnsFrom<Product>()                 .OpenExpression().Where("categoryID").IsEqualTo(5).And("productid").IsGreaterThan(10).CloseExpression()                 .Or("categoryID").IsEqualTo(2).AndExpression("productID").IsBetweenAnd(2, 5)                 .ExecuteAsCollection<ProductCollection>(); Simple Paged Query 
SubSonic.SqlQuery q = Select.AllColumnsFrom<Product>().                Paged(1, 20).Where("productid").IsLessThan(100); Paged Query With Join 
SubSonic.SqlQuery q = new Select("ProductId", "ProductName", "CategoryName").                 From("Products").InnerJoin(Category.Schema).Paged(1, 20); Paged View              SubSonic.SqlQuery q = new Select().From(Invoice.Schema).Paged(1, 20); Simple IN Query 
int records = new Select().From(Product.Schema)                 .Where("productid").In(1, 2, 3, 4, 5)                 .GetRecordCount();             Assert.IsTrue(records == 5); Using IN With Nested Select              int records = Select.AllColumnsFrom
()                 .Where("productid")                 .In(                 new Select("productid").From(Product.Schema)                     .Where("categoryid").IsEqualTo(5)                 )                 .GetRecordCount();  Using Multiple INs 
SubSonic.SqlQuery query = new Select()                 .From(Product.Schema)                 .Where(Product.CategoryIDColumn).In(2)                 .And(Product.SupplierIDColumn).In(3);
