---
layout: post
title: "Using ActiveRecord"
---

# Using ActiveRecord



<h2>Summary</h2>

 
 is the simplest, easiest way to work with your data and your database. The pattern is that each instance you work with is, literally, a row of data in your database. This means that each object type can be thought of as a table in your database.  Many developers don't like to work this "closely" with their database - however others view this kind of thing as absolutely ideal - removing the object-oriented "impedance mismatch" in favor of working with a thin database abstraction.  SubSonic's approach to 
 is to give you what you need, then get out of your way. You'll find you have the ability to use Linq and simple, easy code-generation to get your data quick and simple-like.  

<h2>Setup</h2>

 Setting up SubSonic's 
 is pretty simple and involves four steps.  

<h2>=Add a Reference to SubSonic=</h2>

 Download and extract 
 in a folder like this.  Then inside your project right-click the "Reference" folder, and select Add Reference. Browse to find the SubSonic.Core.dll file and include it.  

<h2>=Add a Connection String=== In order to work with your database you'll need a connection string that is located in your project's app.config or web.config.  If you have a seperate project for your data access code, you may need to create a new app.config in the root of the project.  If you're working with a provider other than SQL Server (such as SQLite), you'll need to specify which one by changing the "providerName" attribute value:<configuration>     ...     <connectionStrings>       <add name="Northwind"           connectionString="server=.\SQLExpress;database=SubSonic;integrated security=true;"           providerName="System.Data.SqlClient"/>       <add name="NorthwindSQLite"           connectionString="Data Source=C:\my.db"           providerName="System.Data.SQLite"/>       <add name="NorthwindMySql"           connectionString="server=localhost;database=northwind;user id=root; password="           providerName="MySql.Data.MySqlClient"/>    </connectionstrings>   </configuration>  ===Set The Connection In The Templates=</h2>

  Look in the Templates folder in the files extracted earlier.  The 
 Templates that create the classes you're going to work with need to know what your connection string is. To set this, open up the file called "Settings.ttinclude". Below the @import statements, you'll see three string values you'll need to change:  
const string Namespace = "Northwind.Data";     const string ConnectionStringName = "Northwind";          //This is the name of your database and is used in naming     //the repository. By default we set it to the connection string name     const string DatabaseName = "Northwind";  "Namespace" refers to the namespace that the generated subsonic code will be placed under.  
namespace Northwind.Data   {     public class YourEntity     {     ...     }   }  You need to fill out "ConnectionStringName" with the connection string value that you placed in your app.config or web.config file earlier.  This tells SubSonic which connection to use in the DB.  Change the "DatabaseName" value to the name of the database specified in the connection string.  The include directive in all *.tt files need to match your database. The ActiveRecord.tt on GitHub master, as of this writing, points to MySQL.ttinclude.  
// other values: MySQL.ttinclude, SQLite.ttinclude <#@ include file="SQLServer.ttinclude" #>  

<h2>=Add the T4 Templates To Your Project=== After you've set the settings above, just drag into your project. Whenever Visual Studio 2008 sees a "tt" file, it will automatically execute it - so you don't have to do anything, it will just run.  List of files to drag:  * ActiveRecord.tt * Context.tt * Settings.ttinclude * SQLServer.ttinclude OR MySQL.ttinclude OR SQLite.ttinclude * StoredProcedures.tt - optional, add if you will invoke stored procedures * Structs.tt  If you make a change to your database, just right-click the ActiveRecord.tt, Context.tt and Structs.tt files (CTRL+Click to select all *.tt files) and select "Run Custom Tool" and this will execute them again.  If you have any errors at this point, you need to check your settings in the prior step.  ==Querying</h2>

 The whole point of using ActiveRecord is to make querying easy. Here are some examples from our unit tests:  
//find a single product by ID var product = Product.SingleOrDefault(x => x.ProductID 

<h2> 1);  //get a list of products based on some criteria var products = Product.Find(x => x.ProductID <= 10);  //get a list of server-side paged products var products = Product.GetPaged(0,10);  //query using Linq var products = from p in Product.All()           join od in OrderDetail.All() on p.ProductID equals od.ProductID           select p;  You'll notice that we've departed a bit from the way SubSonic 2.0 works (as well as other ActiveRecord libraries). Most other libraries use the constructor to pass in the key or name/value pair to find a single record. This can lead to some confusion if there is no record as your object will not be null (as it should be).  For this reason we use a Factory to get single values - as you can see above.  ==Testing</h2>

 Testing with ActiveRecord can be a major pain because it lives "so close" to your database. Rails uses the concept of a Test Database for this - basically saying "get over it" with respect to involving your DB in your unit tests. This can work fine for you - if you want to use a test database you can and ActiveRecord will work fine.  To do this, simply set your connection string in your test project (in the App.config) to point to your test database, and you're good to go.  If you want to have speedier tests with less of a chance of failure due to bad data or connection issues - you can work with SubSonic's built-in testing (for ActiveRecord). There's nothing you need to do other than use the connection string "Test" in your test project:  
<add name="Northwind"           connectionString="Test"           providerName="System.Data.SqlClient"/>  This will tell SubSonic to use a Faked up repository (called TestRepository) which works with a fake set of data. You can set this up as you like using Setup():  
//add 100 products to the fake repository Product.Setup(100); //make sure they're there! Assert.Equal(100,Product.All().Count());  You can also send in the list you want to work with if you want to mock up specific objects. See the constructor overloads for an example.  You will be working against an in-memory List
at this point (based on Setup()), so saving/deleting/editing will add/delete objects in the same way you would see with a database.  

<h2>Changing generated table class names in SubSonic 3</h2>

 Subsonic 2.0 had a feature that was modifiable via the webconfig called 
stripTableText that allowed you to modify the generated class names used by SubSonic.  While not instantly obvious doing the same thing is even simpler and more powerful in subsonic 3 simply by editing the 
Settings.ttinclude file.  The standard empty 
Settings.ttinclude file's 
CleanUp method: 
string CleanUp(string tableName){   string result=tableName;         //strip blanks   result=result.Replace(" ","");         //put your logic here...         return result; }  An simple example of the file edited to change 
 into 
  
string CleanUp(string tableName){   string result=tableName;         //strip blanks   result=result.Replace(" ","");    //strip the phrase "tbl"   result=result.Replace("tbl","");         return result; }  You soon see the simple power for table name manipulation the templates allow.
