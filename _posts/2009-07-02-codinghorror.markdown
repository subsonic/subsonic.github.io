---
layout: post
title: "CodingHorror"
---

# CodingHorror



<h2>Summary== ORMs can never compete with SQL when it comes to data retrieval - it's the difference between object-oriented languages (that deal with object-oriented problems) and language built to work in a relational database system. OO always loses.  You will find yourself, most likely, backed into a situation where you can't get SubSonic to get your data for you. If this is the case and you have a deadline - we got your back. Some people are repulsed by this, others aren't. I've always said that SQL is the best DSL to ever be built for a database - why fight it. Yes it's not the easiest to debug, but neither is your crufty workaround :).  ==Usage</h2>

 I built this aspect of SubSonic specifically for Jeff Atwood, who loves him some SQL. It's use is very, very simple:using(var rdr=new CodingHorror("SELECT * FROM Products WHERE productID=@id",1).ExecuteReader()){    while(rdr.Read()){      //...    } }  You can open up your favorite query tool, create the SQL you need, then paste it right into CodingHorror. You can also make sure it's parameterized (don't want injection!) and if you notice above you can append on parameters, in order, and they will get added to the query.
