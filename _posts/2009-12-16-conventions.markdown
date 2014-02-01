---
layout: post
title: "Conventions"
---

# Conventions



<h2>Philosophy== You hear it a lot: Convention Over Configuration. This is the Ruby On Rails mantra and had a lot of merit. At its core it means that what you do (especially if you've done it a lot) should carry a lot more weight than having to configure (and reconfigure) things over and over.  ==General Conventions==  *Column names should never contain reserved words (system, string, int, etc) *Column names should not be the same as table names  ===Primary Keys=== If you want to use SubSonic to access your table, you need to have a Primary Key defined for your table. This is good practice in every case and we need it to do certain things with your table. If you don't have a Primary Key defined, your class won't be generated.  If you don't believe us, or if you think this is a silly convention - SubSonic isn't for you.  ===Lookup Tables=</h2>

 For lookup tables, the key should be the first column and the "
 the second column. Many of our lookup functions depend on this. Column names such as "ShortDescription" will have labels such as "Short Description" in scaffold.  

<h2>ActiveRecord Specific Conventions==  ===Built-in Auditing=== Every table can have some auditing ability built in, but this is not required.  These fields are:  *CreatedOn (datetime) *CreatedBy (nvarchar(50)) *ModifiedOn (datetime) *ModifiedBy (nvarchar(50))  ===Logical Deletes=== If you want to use logical deletes, you can by adding a field called "Deleted" or "IsDeleted"  ==SimpleRepository Specific Conventions==  * Generated table names will be plural  ===Primary Keys=== If you call a column ID or Key or [ClassName]ID  no matter its type  that will be your Primary Key. If you have other things in mind you can use a primary key attribute [SubSonicPrimaryKey] contained in the SubSonic.SqlGeneration.Schema namespace and well use that column.  ===String length=== There are two ways to tell SubSonic how to handle this  both using attributes. The first is [SubSonicStringLength(int] and the second is [SubSonicLongString] which sets to nvarchar(MAX) or LONGTEXT  depending on your provider.  ===Nullability=== The default is not null, but you can change this by making your propery a nullable type.  ===Numeric Precision=== The default is a Precision of 10 and a scale of 2 but you can change that with the [SubSonicNumericPrecision(int] attribute.      ===Ignoring a Property=</h2>

 You can ignore generation of a property by using [SubSonicIgnore] attribute.
