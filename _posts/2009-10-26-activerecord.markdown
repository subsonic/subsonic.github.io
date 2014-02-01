---
layout: post
title: "ActiveRecord"
---

# ActiveRecord



<h2>What Is Active Record?== SubSonic creates objects for you which reflect your database structure. This is generally called Object-Relational Mapping (OR/M) and while it's true that SubSonic is an OR/M tool of sorts, it does not go the way of normal OR/M tools. You don't have to abide by any rules (never use SPs, etc). You do what you do and we try to make it easier for you and won't think you're fat and stupid.   We love you man.  ==Intelligent Tables== Every table in your database (or the ones you specify in the configuration file) is created as an object by SubSonic, which inherits from the ActiveRecord base class. These objects allow you to push/pull data from your database pretty easily:Product p = new Product(1); Product p = new Product("ProductGUID", "02020-29929-ksk2k-kksksk-anhu3");  ==Typed Collections Pour Vous</h2>

 [DEPRECATED] In addition to the core classes, strongly-typed collections are also generated for you and you can query against these: 
ProductCollection products = new ProductCollection()    .Where("categoryID", 1).Load(); ProductCollection products = new ProductCollection()    .Where("categoryID", 1).OrderByAsc("listOrder").Load();  
  You can load a collection using a reader as well: 
ProductCollection products=new ProductCollection()    .Load(new Query("Products").ExecuteReader());  But doing it this way WILL NOT CLOSE OFF THE READER. This can obviously lead to performance problems. Why you ask? In general, code that calls the reader should close the reader. We wanted to be sure we supported this so we don't close the reader on load of the collections.  You can iterate over the collection easily: 
ProductCollection products=new ProductCollection()   .Where("categoryID",1).Load(); foreach(Product product in products){     //... }  

<h2>Saving Data with ActiveRecord</h2>

 Each object is aware of it's origins - this is the core of ActiveRecord. Each object represents one row in your database, so when you want to save your data, you can simply: 
Product p=new Product(1) p.Name="Changed Name"; p.Save(User.Identity.Name);  The last line with the save method is one of our conventions - passing in who did what when. You can override this if you like.  The Save() method takes a look at an internal state variable called "IsNew". This variable tells the object whether to run an Update() or Insert().  In addition - the query that the database sees will only operate against the columns that have been updated - also known as the "dirty" columns. In this way we save a little burden on the log file and keep things tidy.  

<h2>Deleting Data</h2>

 If you are using logical deletes - delete flags instead of record removal - SubSonic will support this. Our convention is to use "Deleted" or "IsDeleted" as the flag for this column, and that it's a bit field. If you have these fields in your database SubSonic will mark it appropriately on delete, or it will just delete the record.  You can use a permanent delete along with the logical deletes by using "Destroy()".   These methods are static to each object.
