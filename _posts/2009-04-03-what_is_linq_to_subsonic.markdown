---
layout: post
title: "What is Linq to SubSonic"
---

# What is Linq to SubSonic



<h2>Background</h2>

 Language-integrated Query (Linq) is a new feature in C# 3.5 that allows you to work with Functional language programming aspects (lambdas, Func
Expressions, etc) with your code. It can be intimidating at first glance, but once you get used to it, you'll never want to use anything else.  In November of 2008, I rewrote large portions of SubSonic in order to accomodate Linq. This is from my blog post on the subject:  
>SubSonic 3.0 Is... A complete rewrite. The culmination of the things I've learned over the last year as I've (once again) Changed Everything and shared some wonderful Koolaid with my Alt.NET buddies :). Seriously - I've ripped everything out and redone it, with a focus on:  Simpler Lighter Simpler Meaner Simpler Better Faster Simpler  (Not in that order - but generally I've placed an emphasis on simplicity). I've installed interfaces everywhere, and focused on making everything lightweight, testable, and injectable. I hope. We'll see.
  

<h2>Implementation</h2>

 I began the roll from 2.x to 3.0 in the summer of 2008 and immediately I recognized that I was in over my head. When you create a Linq expression:  
var query=from p in db.Products           where p.ProductID=1           select p;  it gets parsed into a recursive unit called an "Expression Tree". This Expression tree is unordered, and each node is a System.Linq.Expression, which can be one of many types of Expression (Lambda, Unary, Binary, Method, Constant, etc) and each of these Expressions can contain 1-n additional Expressions.  It's truly a tree, and it's truly recursive. It's also very difficult to parse properly unless you're very, very familiar with the syntax. Or unless you're   
.  Matt, the initial developer lead for Linq to Sql, has created what he calls the "
" and it's fit the bill perfectly. I tried to write my own expression parser originally - but it's not a very simple thing to do and I failed - three times.  Matt's implementation is very clean and easy to extend. In November of 2008 I was able to run Linq queries against MySQL 5.0. Super awesome.  

<h2>Architecture</h2>

 At it's core, SubSonic 3.0 is: **A SQL/Linq parser **A Simple Query Tool **A Pile of interfaces **A Set of Code Generation Templates that use those interfaces  The main goal of SubSonic 3.0 is to give you the ability to build out your template the 
way you want to. It'a all about taking what we give you and changing it as you need to. I can't stress this enough. 90% of the bug reports we get can be changed by the templates - and that's a good thing. What's better is that you don't need to be stuck by what we do!  

<h2>Flexibility</h2>

 We don't have "a way" of doing something except to keep it as simple as possible. Hopefully you can see that in all of our tutorials.   Currently there are 3 ways to talk to a database: **Linq **Simple Query Tool **Inline (aka CodingHorror)  The last thing we want to do is to impose our silly thoughts on your work day - we want to help you to get home early!
