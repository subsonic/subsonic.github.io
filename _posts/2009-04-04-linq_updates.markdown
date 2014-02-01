---
layout: post
title: "Linq Updates"
---

# Linq Updates



<h2>Summary</h2>

 You can use the goodness that is the Linq syntax to update data inyour database. It's important to note that SubSonic IS NOT AN ORM - it's a query tool (subtle difference) and therefore it doesn't do object tracking. There's nothing stopping you from 
. This is fine and dandy if you like working that way - but we think this is a Big Lie.  The web is a stateless medium - this sort of "contextual tracking" is just not the Real World and we don't drink that beer.  

<h2>Setup== Make sure you setup SubSonic by adding a reference, setting up your DB connection, and then adding the templates to your project.  ==Simple Updates</h2>

 You can work directly against the 
     .Set(x => x.UnitPrice 

<h2> 100, x => x.ProductName == "Test")     .Where(x => x.ProductID </h2>

 1).Execute();  This will produce this SQL statement:  
UPDATE [Products] SET UnitPrice=@up_UnitPrice, ProductName=@up_ProductName  WHERE ProductID = @0  

<h2>Using The Repository</h2>

 Many people don't want to write this stuff by hand and would rather use objects. You can definitely do this by using our 
, which is generated for you if you using our default T4 templates.  

<h2>=Simple Updates=</h2>

 This update statement will work using our 
: 
var repo = new NorthwindRepository<Product>(); Product p = repo.Find(x => x.ProductID 

<h2> 5).SingleOrDefault(); p.UnitPrice = 1000; repo.Update(p);  ===Multiple Updates=</h2>

 You can use our IRepository to queue up a batch of changes (transactionally) but saving your objects to a list, then passing them to Update: 
var repo = new NorthwindRepository<Product>(); var queue = new List<Product>();  for (int i = 0; i < 10; i++) {     Product p = repo.GetByKey(i);     p.UnitPrice = 1000;     queue.Add(p); } repo.Update(queue);
