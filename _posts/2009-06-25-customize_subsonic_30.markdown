---
layout: post
title: "Customize SubSonic 3.0"
---

# Customize SubSonic 3.0



<h2>Summary</h2>

 Customizing SubSonic for your own use is meant to be easy. Initially you will probably focus on using our templates to get you going, but a little introspection into how we do what we do and you'll see that creating your own approach is rather simple.  It's our hope that if you make a killer set of templates, you'll 
.  

<h2>Concepts</h2>

 There are 3 main things you need to know about SubSonic: *SubSonic will parse Expressions into SQL for you *SubSonic will handle the data connections for you using it's Provider setup (note: this isn't the same ProviderModel as before. A provider is a connection string) *
 will generate the code you need  These are the foundations for each data access template we've created.  

<h2>IQueryable Expression Parser</h2>

 Working with SubSonic's expression parser is very, very easy. To show this, let's start with a class called "Post":public class Post{    public Guid ID {get; set;}    public string Title {get; set;}    public string Body{get; set;} }  If there is a table in the database that corresponds to this class, we can access it by setting up a Provider and then a Query to go along with it.  The Provider setup goes like this: 
var provider=SubSonic.DataProviders.ProviderFactory             .GetProvider(connectionString, providerName)  In this example we've passed in the connection string and the provider name ("System.Data.SqlClient", for instance) - but you can pass nothing in and we'll do our best to pull the connection string out (it helps if you only have one defined). Or you can pass the name of the connection string, and we'll use the providerName set from it.  Setting the providerName is pretty important - it tells System.Data.Common (the core data access we use) which runtime ADO provider to use. If you don't pass it along, we'll assume you mean SQL Server.  Next up, you create the Query, passing along the provider to use:  
var query=new Query<Post>(provider);  Putting it all together, it looks like this: 
var provider=SubSonic.DataProviders.ProviderFactory             .GetProvider(connectionString, providerName) var query=new Query<Post>(provider); var posts=from p in query           where p.Title.StartsWith("M")           select p;  It's that simple to create an IQueryable call using SubSonic. But that isn't the only way to interrogate your database - you can also use the 
 or our inline SQL tool: 
.  

<h2>Putting It Together With T4</h2>

 There are lots of ways to push the core pieces around to generate your data access. The best place to start is to have a look at our existing templates: *
 *
  These are built for you to extend and tweak and if you want to know more, read up on 
.  
" that accepts a tableName. This method currently replaces empty spaces with underscores - but you can have it do whatever you like with respect to naming.  In addition, there is a string array called "ExcludeTables" that you can add certain tables to and they won't be generated as classes.  As you can see from this - the code is wide open and there for you to change and tweak as needed. Our templates are simply a starting point for you.   

<h2>Creating Your Own Templates</h2>

 We've put together a whole page on how you can leverage the SubSonic core bits to use with T4 - have a read on 

