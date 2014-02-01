---
layout: post
title: "Supported Databases"
---

# Supported Databases



<h2>SubSonic 2.x== Subsonic 2.2 Currently supports 5 main database engines: *SQL Server (2000 through 2008) *MySQL (5.0+) with special support for InnoDB *Oracle - although we've had reports of some issues with Foreign Keys and Stored Procedures *SQL CE (Compact Edition) *SQLite  We develop everything using SQL Server 2005, so you might fight an optimal experience using this with SQL.  ==SubSonic 3.0== ===Currently supported=</h2>

 SubSonic supports and has templates for:  *SQL Server (2000-2008) *MySQL (5.0 +) *SQLite *Oracle support through ODP.NET is currently in development. You can get the latest version of the SubSonic core from 
. The templates are also available 
. Please post details of any issues or questions to the 
 is currently in development. You can get the latest version of the SubSonic core from 
. The templates are also available 
. Please post details of any issues or questions to the 
.  

<h2>=What about other databases?=</h2>

 Our goal with SubSonic 3.0 was to unhinge the core from any dependency on a specific engine. We do this by using System.Data.Common - which is part of Microsoft's DataFactory stuff. Most major databases have a provider which works with System.Data.Common - including:  *PostGres *SQL CE *VistaDB  SubSonic will execute queries against these databases, however we're still working on creating a meaningful set of templates for each.  It's important to understand that SubSonic 3.0 talks to the database when creating your Data Access stuff using our 
, SQL Server will return a completely different result set than MySQL. This is supposed to be a standard - but there are obviously deviations with each provider.  Our SQL Server templates query INFORMATION_SCHEMA - an ANSI-standard set of system views that each provider should offer for each database. However MySQL doesn't implement them in the same way SQL Server does - so we can't provide a "single template fits all" scenario.  It's our hope that our 
 - so if you take the time to create a nice set of templates - please add to our wiki!
