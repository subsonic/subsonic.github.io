---
layout: post
title: "Selecting Templates"
---

# Selecting Templates



<h2>Summary== With choice comes trouble - sometimes it's just easier to do what the tool tells you to do (hammer says "hit nail"). SubSonic's not really that way - our goal is to give you as many different ways as you need to work with your data - our goal is to help, not tell you what to do. So we lend a hand and get out of your way.  That said - here's a summary of what each approach does for you with SubSonic 3.0.  ==ActiveRecord</h2>

 
 is especially simple to work with, and abstracts the most for you. Your objects are generated from the tables in your database, with IQueryable foreign keys. You can work with Linq if you like, or you can save some time working directly with Factory methods for getting data.  
 also mocks out your database automatically by setting your connection string to "Test". This will allow you to work against in-memory lists rather than hit the database.  You can read more about 
 here.  

<h2>SimpleRepository</h2>

 If code generation is not your thing and your database is there to (mostly) store your application's data - then SimpleRepository is for you. Many applications (like a Blog, for example) have a very light "need" when it comes to storing data - so why use a massive data access pattern?  
.  With SimpleRepository you're working with POCOs - not an object set that is built on a heavy base class. For many this is optimal.  

<h2>Linq Templates</h2>

 This template set was the original build for SubSonic's 
 Template approach, and approximates, to a high degree, Linq To SQL's approach to data access.  This set of templates is somewhere between SimpleRepository and ActiveRecord: you get to work with POCOs but you also have a nice degree of abstraction using some basic code generation.
