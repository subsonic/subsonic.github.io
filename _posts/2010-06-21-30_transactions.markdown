---
layout: post
title: "3.0 Transactions"
---

# 3.0 Transactions



<h2>Summary== Transactions are a core need for many application developers and involve executing a set of directions in a "all or nothing" manner - meaning that if one instruction fails - the whole thing fails.  ==Considerations== The easiest thing to do is to use System.Transactions to wrap a "TransactionScope" around whatever it is you're doing. To make this work, however, you'll need to have the Distributed Transaction Coordinator (DTC) running on your server.  You can get around this, however, by "suppressing" the "elevation" to DTC (which ADO will do for you if it's confused as to what's needed) by using our "SharedDbConnectionScope" (see below).  ==Example of Using Scope== Executing Transactions using SubSonic is a matter of wrapping a scope around a section of code (using System.Transactions):using (SharedDbConnectionScope sharedConnectionScope = new SharedDbConnectionScope()){    using (TransactionScope ts = new TransactionScope())    {        Product p = new Product.SingleOrDefault(x=>x.ProductID==1);        p.Title = "new title";         Product p2 = new Product.SingleOrDefault(x=>x.ProductID==2);        p.Title = "another new title";         // ...        p.Save();        p2.Save();        ts.Complete();   } }  ==Using Built-in Methods</h2>

 There are other ways of working with transactions in SubSonic, and if you're worried about using the DTC then you might want to consider using the built in tools, specifically the 
.
