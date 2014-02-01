---
layout: post
title: "3.0 Multiple Databases"
---

# 3.0 Multiple Databases



<h2>Summary== If you need to change your connection string on the fly, there are a few ways you can do this. SubSonic 3.0 supports both - there is only one way to do it with SubSonic 2.0.  ==Using SharedDbConnectionScope== Normally when executing a query (reader or list) the default provider is used. However you can override this by using a SharedDbConnectionScope:using (var scope = new SharedDbConnectionScope("server=localhost;database=Northwind;user id=root;password=;", "MySql.Data.MySqlClient")) {          //this will execute against MySQL - not whatever the default provider is     //in the web/app.config     var rdr= new CodingHorror("SELECT * FROM Products").ExecuteReader();       }  ==Using Built-in Switching (3.0 only)</h2>

 You can change the underlying Connection at any time with SubSonic 3.0 by changing providers at runtime, or by passing in the connection string information. Using our 
 templates, this looks like:  
var product=Product.SingleOrDefault(x=>x.ProductID==1,"server=.\SQLExpress; ...","System.Data.SqlClient"); product.Save("server=localhost...","MySql.Data.MySqlClient");  It goes without saying that normally you wouldn't want to do this - but in some situations (a hosted app, for instance) you might want to set this stuff on the fly - sending in variables rather than string values.  If this doesn't work for you, remember you can always tweak the templates to your needs.
