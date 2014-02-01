---
layout: post
title: "Querying Views"
---

# Querying Views

Views are supported as read-only objects in SubSonic. You can't update or save information from a view, but these objects are super handy when you have complex data structures. Querying them is exactly the same as with tables, and you have full strongly-typed collection support as well.  In general, Views can cause confusion in your application between developers on your team. Invariably business logic will tend to creep in, and those unfamiliar with SQL will be at a disadvantage in your group. We strongly suggest you let the query tool work to your advantage and don't use Views. You'll sleep better at night.
