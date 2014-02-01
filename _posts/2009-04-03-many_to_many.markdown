---
layout: post
title: "Many to Many"
---

# Many to Many

Many to Many joins are joins between tables that are "non-structural" and instead, are logical. This means that the relationship is not necessarily enforced by your database engine and must be handled in code for the most part (this is only sort of true).  For instance, if you have a Products table that can have one or more Categories assigned to it, and a Categories with one or more Products assigned to it, you have a Many to Many. To facilitate this structure in your database you need a "joining" or "mapping" table, which has a composite primary key made up of the primary key of the main tables - so in this example it would be ProductID and CategoryID together defining the primary key.  You don't have to do it this way, but if you do SubSonic will love you for it because we can then spin some magic up for you.
