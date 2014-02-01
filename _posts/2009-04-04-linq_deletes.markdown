---
layout: post
title: "Linq Deletes"
---

# Linq Deletes



<h2>Summary</h2>

 You can use the goodness that is the Linq syntax to delete data from your database. It's important to note that SubSonic IS NOT AN ORM - it's a query tool (subtle difference) and therefore it doesn't do object tracking. There's nothing stopping you from creating a 
. This is fine and dandy if you like working that way - but we think this is a Big Lie.   The web is a stateless medium - this sort of "contextual tracking" is just not the Real World and we don't drink that beer.  

<h2>Setup</h2>

 Make sure you 
 SubSonic by adding a reference, setting up your DB connection, and then adding the templates to your project.  

<h2>Simple Deletes</h2>

 You can work with the 
;  This creates the following SQL: 
DELETE FROM [dbo].[Products]  WHERE [dbo].[Products].[ProductID] = @0  

<h2>Using the Repository</h2>

 There are 2 ways to delete using the IRepository generated for you: 
var repo = new NorthwindRepository<Product>(); repo.Delete(1);  //OR var repo = new NorthwindRepository<Product>(); var product = repo.GetByKey(1); repo.Delete(product); 

<h2>=Multiple Deletes=</h2>

 You can delete multiple objects transactionally using Batch Query: 
var repo = new NorthwindRepository<Product>(); var queue = new List<Product>(); for (int i = 1; i < 10; i++) {     var product = repo.GetByKey(i);     queue.Add(product); } repo.Delete(queue);
