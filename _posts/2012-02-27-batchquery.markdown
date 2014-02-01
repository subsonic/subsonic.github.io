---
layout: post
title: "BatchQuery"
---

# BatchQuery



<h2>Summary== Sometimes you have a routine that needs to make multiple calls to a database, which can be a bit of a drain on resources if you're opening/closing connections each time. This can happen when running multiple pass-through queries (UPDATES, INSERTS, DELETES) or if you need multiple different result sets.  BatchQuery can help in this regard - allowing you to execute multiple pass-throughs in a single transation or as a single statement. You can also execute SELECTs using multiple result sets.  ==Considerations== Sometimes it's not a good idea to return multiple result sets, or to execute multiple queries, using a single connection. This section discusses some things to consider.  If you batch together multiple calls into a single SQL statement, you can inadvertantly hold open a connection to your database for longer than you desire. This can end up in optimistic locking problems, or, if you're using something like SQLite, can lockup your entire database, causing issues for your application.  Finally, some providers don't allow you to use multiple result sets (called MARS). You should find out from your provider if it supports multiple return sets.  In addition, concurrency issues can creep up if the calls are not executed fast enough. Use this feature with caution.  ==Creating a Batch Query== To create BatchQueury, you need to create a provider (which is a glorified connection string wrapper) and then a BatchQuery:var provider=ProviderFactory.GetProvider("Northwind"); var batch=new BatchQuery(provider);  ==Executing Multiple Selects</h2>

 Once you have created your BatchQuery, you can now "queue" the queries you want to execute in one call. The BatchQuery will translate each query into a single SQL statement, executed with one command:  
var provider=ProviderFactory.GetProvider("Northwind"); var batch=new BatchQuery(provider);  var query1=from p in db.Products            where p.ProductID

<h2>1            select p; batch.Queue(query1);  var query2=from p in db.Products            where p.ProductID</h2>

2            select p; batch.Queue(query2);  using(var rdr=batch.ExecuteReader()){         if(rdr.Read()){        //query1 results     }     rdr.MoveNext();     if(rdr.Read()){        //query2 results     } }  You can queue IQueryable or 
.  

<h2>Executing Multiple Pass-through Queries== There are 2 ways to do this - with a transaction or without.   ===Using a Transaction=</h2>

 Probably the best way to execute multiple updates at once is to use a transaction to be sure that every update goes through. To do this, work up your query and use "QueueForTransaction()":  
var provider=ProviderFactory.GetProvider("Northwind"); var batch=new BatchQuery(provider);  var query1= new SubSonic.Query.Update<Product>(provider)            .Set(x => x.CategoryID 

<h2> 5)            .Set(x => x.UnitPrice == 100)            .Where(x => x.ProductID == 1);  batch.QueueForTransaction(query1);  var query2= new SubSonic.Query.Update<Product>(provider)            .Set(x => x.CategoryID == 1)            .Set(x => x.UnitPrice == 200)            .Where(x => x.ProductID == 2);  batch.QueueForTransaction(query2);  //execute transaction batch.ExecuteTransaction();  ===Using a Single SQL Statement=</h2>

 You can write the same queries above, however insteading of using "QueueForTransaction" you can just use "Queue" and then when it comes to execution, just use "Execute()". This will produce the following SQL:  
UPDATE [dbo].[Products]  SET [dbo].[Products].[CategoryID]=5, [dbo].[Products].[UnitPrice ]=100, WHERE [dbo].[Products].[ProductID ]=1;  UPDATE [dbo].[Products]  SET [dbo].[Products].[CategoryID]=1, [dbo].[Products].[UnitPrice ]=200, WHERE [dbo].[Products].[ProductID ]=2
