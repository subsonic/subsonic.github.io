---
layout: post
title: "Using AdvancedTemplates"
---

# Using AdvancedTemplates



<h2>Summary==  ==Setup</h2>

 Setting up SubSonic's 
 is pretty simple and involve's 4 steps.  

<h2>=Add a Reference to SubSonic=== This part is pretty simple: right-click your project, Add Reference, and Browse to find the SubSonic 3.0 dll.  ===Add a Connection String=== In order to work with your database you'll need a connection string. If you're working with a provider other than SQL Server (such as SQLite), you'll need to specify which one using "providerName":<add name="Northwind"           connectionString="server=.\SQLExpress;database=SubSonic;integrated security=true;"           providerName="System.Data.SqlClient"/>      <add name="NorthwindSQLite"           connectionString="Data Source=C:\my.db"           providerName="System.Data.SQLite"/>     <add name="NorthwindMySql"           connectionString="server=localhost;database=northwind;user id=root; password="           providerName="MySql.Data.MySqlClient"/>  ===Set The Connection In The Templates=</h2>

 The 
 Templates that create the classes you're going to work with need to know what your connection string is. To set this, open up the file called "Settings.ttinclude". Below the @import statements, you'll see three settings you'll need to set:  
const string Namespace = "Northwind.Data";     const string ConnectionName = "Northwind";          // This is the name of your database and is used in naming the repository.     const string DatabaseName = "Northwind";  The main one you need to set is "ConnectionName" - this tells SubSonic which connection to use in the DB. The namespace constant is the namespace of the classes that SubSonic will generate.  

<h2>=Add the T4 Templates To Your Project=== After you've set the settings above, just drag into your project. Whenever Visual Studio 2008 sees a "tt" file, it will automatically execute it - so you don't have to do anything, it will just run.  If you make a change to your database, just right-click the SubSonic3Creator.tt file and select "Run Custom Tool" - this will execute it again.  As opposed to the ActiveRecord template - the AdvancedTemplate uses the T4 Toolkit to do some fancy stuff - including outputting a file for each class (many people like this) and also creating a generation log so you know what it's doing.  ==Querying</h2>

 Querying the AdvancedTemplates works just like Linq to Sql:  
var db = new Northwind.Data.NorthwindDB(); var qry = from p in db.Products           select p;  In this example, "db" is akin to Linq to Sql's DataContext (what we call a "
 - but all it does is expose the tables in your database as IQueryable
- it does not do any "UnitofWork" or change tracking.  You can also use the 
 to use SubSonic's existing query tool:  
var db = new Northwind.Data.NorthwindDB(); var products = db.Select.From<Northwind.Data.Product>()     .ExecuteTypedList<Northwind.Data.Product>();  

<h2>Testing</h2>

 The AdvancedTemplates center on an implementation of 
 - which is essentially a query contract for you to work with your database. You can mock this using your favorite mocking tool, or create a Fake if that makes more sense.
