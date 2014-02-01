---
layout: post
title: "Writing Testable Code With SubSonic 2.1"
---

# Writing Testable Code With SubSonic 2.1



<h2>Summary== Note: this is for SubSonic 2.1  ActiveRecord is not the most testable thing in the world :). I've really tried to push SubSonic into the TDD realm and thought it might be a good idea to show how you can structure up a highly testable, decoupled application using SubSonic as your Data Access tool.  ==The Repository Pattern</h2>

 This is usually the first choice in Data Access patterns when it comes to writing testable, decoupled code. So I'm going to use that today. If you arent' familiar with it, you may want to 
. Essentially, the idea here is that you want to abstract your data access/query bits as much as possible from the rest of your application - including your model.  

<h2>Data Access</h2>

 Let's assume, for now, that I'm writing tests for everything I do. And my tests tell me that I need to setup a Catalog Repository that talks to my DB (for today it will be Northwind). My tests tell me I need to have a Product so the first thing I do is setup a class to represent a Product:public class Product {          public int ProductID { get; set; }         public string ProductName { get; set; }         public decimal UnitPrice { get; set; }      } Next, I need to have a method on my Repository that will retrieve products from the DB. I define an interface that will abstract the implementation of the Repository: 
public interface ICatalogRepository {          IList<Product> GetProducts();      }  Finally, I need to setup an implementation of this interface, and it will use SubSonic. I reference and setup SubSonic in the Data Access class, and then generate all the good stuff SubSonic will create for me here. Note that I can use 
 or 
 - it doesn't matter, and that's just how I want it.   All I'm going to use is the 
.  

<h2>Mapping</h2>

 If you're not use to using ORM tool (Object-Relational Mappers), you may not know why I want to "duplicate" the classes that SubSonic generates, versus the one I created here in my "Model" folder.  The reason comes down to what's known as "impedance mismatch" - the idea that my DB structure will not follow my application structure (and therefore OO principles). Moreover, if you tie your DB structure to your application, eventually you will end up with some pain points as your DB grows - and to mitigate these you compromise good DB practices. The opposite is true as well - you "bend" your application to allow for easier use of the DB. I'll end this discussion here :).  What I need to do now is implement ICatalogRepository using SubSonic, and map the Northwind Products to my Model. This is easy to do with SubSonic, using "ExecuteTypedList": 
public class SubSonicCatalogRepository:ICatalogRepository {          public IList<Product> GetProducts() {              return Northwind.DB.Select("ProductID", "ProductName", "UnitPrice")                 .From<Northwind.Product>().ExecuteTypedList<Product>();           }     }   ExecuteTypedList tries to match the names of the returned columns to the names of the properties of the passed-in type. In this example they match exactly - and that's not completely real world. You can get around this by aliasing the columns - in the same way you'd alias a SQL call: 
return Northwind.DB.Select("ProductID as 'ID'", "ProductName as 'Name'", "UnitPrice as 'Price'")                 .From<Northwind.Product>().ExecuteTypedList<Product>();   Note: Using "as" is ANSI SQL, and will work with most DB providers - including MySQL 5.x and above.  You can also Stored Procedures here, or Views - up to you.  

<h2>The Test</h2>

 In the Test Application, all you need to do is:  **Reference your Data Access project  **Setup SubSonic's configuration (since this is an execution end point)  Note that I don't have to reference to SubSonic in my test application. I don't need it - it's abstracted nicely away. Now I can write my tests, stubbing out ICatalogRepository with a TestCatalogRepository, and use Dependency Injection to inject the SubSonicCatalogRepository as needed :).  To make sure that SubSonic is playing nicely here, you can write an integration test: 
[TestMethod]         public void SubSonic_Should_Return_Product_List() {              ICatalogRepository rep = new SubSonicCatalogRepository();             IList<Product> products = rep.GetProducts();             Assert.AreEqual(77, products.Count);         }  

<h2>Putting it All Together</h2>

 The key to making this work is the Dependency Injection Pattern - the ability to pass a dependency to another class through its constructor using an interface.   To get this all to work, you need to create a business logic class (or some class which will use the data access bits) and then pass the repository in. In this example, I have a CatalogService, which will take an ICatalogRepository: 
public class CatalogService {          ICatalogRepository _repository;         public CatalogService(ICatalogRepository repository) {             _repository = repository;         }          public CatalogService(){             _repository = new SubSonicCatalogRepository()         }          public IList<Product> GetProducts() {             List<Product> products = _repository.GetProducts();                          //inventory checks              //discount setups              //cross-sell correlation              //bundling...          }      }  The deal here is that by default, our CatalogService will use SubSonic. For testing, however, we can "inject" a fake or a mock into this class so we don't need to hit the database.
