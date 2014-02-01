---
layout: post
title: "SubSonic 3 Frequently Asked Questions"
---

# SubSonic 3 Frequently Asked Questions

##[Summary]()

  Answers to some of the more common questions asked about SubSonic asked on stackoverflow.  

<h2> General SubSonic questions ==  === How do I extend the generated SubSonic classes? =</h2>

  All the generated SubSonic classes are partials so all you need to do to add extra properties/methods to them is to create your own partial class with the same name in the same namespace and the two will be merged at compile time. For example you extend the a generated Customer class as follows:  
public partial class Customer {   public string FullName   {     get      {        return // Format and return the customer's full name here     }    } }   
  

<h2>= How do I know if a database operation has succeeded? =</h2>

  Unless a 
 is thrown then the operation has succeeded.  
  

<h2>= How do I fix the error "Metadata file 'System.Data.SQLite' could not be found"? =</h2>

  Make sure you have SQLite installed on your machine and the 
 referenced in your project.  
  

<h2>= How do I add DataAnnotations to my generated class? =</h2>

  You need to create a 
 and apply the Data Annotations to that class:  
[MetadataType(typeof(ContactValidation))] public partial class Contact { }  public class ContactValidation {   [DataType(DataType.EmailAddress, ErrorMessage = "Please enter a valid email address")]   public string Email { get; set; } }  
  

<h2>= How do I use a transaction? =</h2>

  
  

<h2>= My Table/Column names are causing problems. How can I get round this? =</h2>

  The CleanUp() function was built for this - it's in Settings.tt. You should be able to rename your class as needed.  
  

<h2>= How can I retrieve just the value of one column from a table? =</h2>

  To do this using Linq:  
var query = from customer in Customer.All()   select new {     customer.CustomerAddress   }   
  

<h2>= Why aren't the t4 templates working? =</h2>

  If the templates don't run automatagically you should just be able to right click on them and choose 'Run custom tool'. If that doesn't work it's probably because of one of the following:  * The first thing to check is whether you're using an Express version of Visual Studio. If so t4 templates aren't supported and you're going to have to do some work. Have a look at 
 stackoverflow question to see what you need to do.   * If you're not using Express then the next possible cause is that you're trying to run the templates inside a Website project rather than a Web Application Project and t4 templates won't work in a Website project. If this is the case then just add a Library project to your solution and drop the templates in there instead.   * Sometimes a broken Visual Studio installation will cause t4 integration to stop working. In this case unfortunately only a reinstall will fix things for you but before you try that it's always worth posting a question to 
.
