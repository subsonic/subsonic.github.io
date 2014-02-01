---
layout: post
title: "Using SimpleRepository"
---

# Using SimpleRepository



<h2>Summary</h2>

 Most data access libraries work from "the database outward" - meaning that one way or another your database tables are represented as objects in your application. This can work in many cases, but relational theory does not align with object-oriented programming, and you get into a hole which is commonly referred to as "the impedance mismatch".  Many people like to work with classes and don't want to worry about the database implementation - freeing them to work as they want to work without opening up a database designer in order to model their classes. The objects they create a free of base classes and exist on their own, as plain-old CLR objects (also known as POCOs).  If you're one of these people and you don't particularly care about the database structure - the 
 is for you.  

<h2>Screencast== Couldn't help myself... love to make these things... <ag> subsonic_migrations.flv </ag>  ==Setup</h2>

 Setting up the 
 is part of the fun of using it in that all that's involved is adding SubSonic and a connection string. The focus is getting completely out of your way.  

<h2>=Add a Reference to SubSonic=== This part is pretty simple: right-click your project, Add Reference, and Browse to find the SubSonic 3.0 dll.  ===Add a Connection String=== In order to work with your database you'll need a connection string. If you're working with a provider other than SQL Server (such as SQLite), you'll need to specify which one using "providerName":<add name="Northwind"           connectionString="server=.\SQLExpress;database=SubSonic;integrated security=true;"           providerName="System.Data.SqlClient"/>      <add name="NorthwindSQLite"           connectionString="Data Source=C:\my.db"           providerName="System.Data.SQLite"/>     <add name="NorthwindMySql"           connectionString="server=localhost;database=northwind;user id=root; password="           providerName="MySql.Data.MySqlClient"/>  You're done!  ==Auto Migrations</h2>

 One of the fun things about working with Rails is that you can build your DB from code and focus on your app. Many developers have found this very freeing (myself included). One drawback to it, however, was that you needed to learn the code for the Migration, and you needed to know how it worked. This, to me, was not a show-stopper in the least but I always wished Rails would "just know" and migrate stuff for me.  This is what I'm trying to do with Auto Migrations using SubSonic. The goal here is if you set a flag in the SimpleRepository constructor, you can tell it to migrate your model for you - automatically creating and synchronizing your database for you.  The key to this is setting the proper options in the constructor:  
var repository=new SimpleRepository(SimpleRepositoryOptions.RunMigrations);  Setting this to RunMigrations tells SubSonic to migrate your model object to the database whenever you try to access the database or save data.  

<h2>=Migration Example=</h2>

 Suppose you have an object called Post: 
public class Post{    public Guid ID {get; set;}    public string Title {get; set;}    public string Body{get; set;} }  When you use this object with the SimpleRepository, assuming you've set the options to RunMigrations, it will create the tables you need: 
//create a new repository for BlogDB database, turning migrations on var repo=new SimpleRepository("BlogDB",SimpleRepositoryOptions.RunMigrations); var post=repo.Single<Post>(x=>x.Title="My Title");   In this example there is no post with this title, since there is no Posts table. The Single() method, however, will run the migration for you and will create the table - so there will be no error.  When run for the first time, the following SQL will be executed prior to the SELECT: 
CREATE TABLE [Posts] (   [ID] uniqueidentifier NOT NULL PRIMARY KEY,   [Title] nvarchar(255) NOT NULL,   [Body] nvarchar(255) NOT NULL, ); ALTER TABLE [Posts] ADD CONSTRAINT PK_Posts_Key PRIMARY KEY([ID])";  Notice that the table name is pluralized (by convention), the "ID" property is selected as the key (again by convention), and the strings are defaulted to a length of 255.  You can change the way SubSonic creates the table by using a small set of attributes - specifically:  *
: If you call a column ID or Key or [ClassName]ID  no matter its type  that will be your Primary Key. If you have other things in mind you can use a primary key attribute (SubSonicPrimaryKey) and well use that column. *
: There are two ways to tell SubSonic how to handle this  both using attributes. The first is SubSonicStringLength(int length) and the second is SubSonicLongString which sets to nvarchar(MAX) or LONGTEXT  depending on your provider. *
: The default is not null, but you can change this by making your property a nullable type. *
: The default is a Precision of 10 and a scale of 2 but you can change that with the SubSonicNumericPrecision(int precision, int scale) attribute. *
: you can ignore generation of a property by using SubSonicIgnore attribute.  
Updating Your Model Starting out is the easy part, but as you develop you will be changing and removing properties from your class. SubSonic will do its best to keep up with you.  For example, let's say you've added a PublishDate to your Post class: 
public class Post{    public Guid ID {get; set;}    public string Title {get; set;}    public string Body{get; set;}    public DateTime PublishDate {get;set;} }  When you next Save/Find/Get data using the SimpleRepository, the following command will be sent along first:  
ALTER TABLE [Posts] ADD DateTime datetime NOT NULL CONSTRAINT DF_Posts_PublishDate DEFAULT ('01/01/0001'); UPDATE SubSonicTests SET PublishDate ='01/01/0001';  There are a few things happening here. The first is that the column is added for you (with NOT NULL - which you can change by using DateTime?). The second is that a default is put in place for you (using DateTime.MinValue) - a non-null column should have a default value in general (our convention).  The UPDATE statement is there to deal with existing records that might be in the database already - setting their value to the default (for other providers like SQLite and MySQL).  Continuing on - removing a property will result in the column being dropped from the database.  

<h2>Querying</h2>

 You can query your database through the repository quite easily, even using Linq if you like:  
var repo=new SimpleRepository(SimpleRepositoryOptions.RunMigrations);  //see if a record exists bool exists=repo.Exists<Post>(x=>x.Title

<h2>"My Title");  //use IQueryable var qry=from p in repo.All<Post>()         where p.Title=="My Title"         select p;  //get a post var post=repo.Single<Post>(x=>x.Title=="My Title"); var post=repo.Single<Post>(key);  //a lot of posts var posts=repo.Find<Post>(x=>x.Title.StartsWith("M"));  //a PagedList of posts - using 10 per page var posts=repo.GetPaged<Post>(0,10); //sort by title var posts=repo.GetPaged<Post>("Title",0,10);  //add a post var newKey=repo.Add(post);  //add a lot of posts - using a transaction IEnumerable<Post> posts=GetABunchOfNewPosts(); repo.AddMany(posts);  //update a post repo.Update(post);  //update a bunch of posts in a transaction IEnumerable<Post> posts=GetABunchOfNewPosts(); repo.UpdateMany(posts);  //delete a post repo.Delete<Post>(key);  //delete a lot of posts repo. DeleteMany <Post>(x=>x.Title.StartsWith("M"));  //delete posts using a transaction IEnumerable<Post> posts=GetABunchOfNewPosts(); repo.DeleteMany(posts);  ==Testing</h2>

 Testing with SimpleRepository is very simple as it inherits from SubSonic.Repository.IRepository. If you follow an injection pattern whereby you pass in an IRepository, then you can use your favorite mocking tool or create a fake repository to query against.
