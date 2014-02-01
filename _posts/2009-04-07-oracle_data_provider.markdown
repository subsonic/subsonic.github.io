---
layout: post
title: "Oracle Data Provider"
---

# Oracle Data Provider

One of the main things to note when using the Oracle Data Provider is that the Foreign Keys are not created for the classes when they are generated when using Subcommander to generate your classes, as such you will need to specify what columns you are joining on in you your Queries see below for an example.  Example of Join using Oracle Data ProviderCustomerCollection customersByCategory = new Select()                 .From(Customer.Schema)                 .InnerJoin(Order.CustomerIDColumn, Customer.CustomerIDColumn)                 .InnerJoin(OrderDetail.OrderIDColumn, Order.OrderIDColumn)                 .InnerJoin(Product.ProductIDColumn, OrderDetail.ProductIDColumn)                 .Where("CategoryID").IsEqualTo(5)                 .ExecuteAsCollection<CustomerCollection>();  Left Outer Join 
SubSonic.SqlQuery query = DB.Select(Aggregate.GroupBy("CompanyName"))                 .From(Customer.Schema)                 .LeftOuterJoin(Order.CustomerIDColumn, Customer.CustomerIDColumn);   

<h2>Features not supported by Oracle</h2>

 **Top  -Oracle does not support the "TOP" key word and though SubSonic is magic it doesn't add this functionality to Oracle
