---
layout: post
title: "IQueryable"
---

# IQueryable



<h2>Summary</h2>

 Working with IQueryable is not easy if you're doing it from scratch, but creating your own using SubSonic's core is pretty easy and can help you 
 SubSonic nicely.  

<h2>Create a Provider== This is not a ProviderModel provider - it's a SubSonic "wrapper" for a connection string and allows SubSonic to know how to connect to your DB and which provider to use. It's easy to create a provider://get a provider for the northwind connection in our Web.config var provider=SubSonic.DataProviders.ProviderFactory.GetProvider("Northwind");  //get a provider based on this passed-in connection string and provider name var provider=SubSonic.DataProviders.ProviderFactory              .GetProvider("server=..","System.Data.SqlClient");  //get a provider based on the only connection string in the Web or App.config var provider=SubSonic.DataProviders.ProviderFactory.GetProvider();  ==Create an Object</h2>

 To use IQueryable, you have to define an object on which to query. Our Expression Parser will then turn that into SQL: 
public class Post{    public Guid ID {get; set;}    public string Title {get; set;}    public string Body{get; set;} }  ==Create the Query
== Finally, to create an IQueryable for your object, simply create a Query
and query it:  
var provider=SubSonic.DataProviders.ProviderFactory             .GetProvider(connectionString, providerName) var query=new Query<Post>(provider); var posts=from p in query           where p.Title.StartsWith("M")           select p;  

<h2>Doing It In One Line</h2>

 If you only have one connection string you can shorten this whole thing to one line: 
var posts=from p in new Query<Post>()           where p.Title.StartsWith("M")           select p;
