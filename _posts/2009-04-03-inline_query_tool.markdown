---
layout: post
title: "Inline Query Tool"
---

# Inline Query Tool

Sometimes there's just no way an ORM can do what you want it to do, and I completely recognize this. It's just not a good idea to try to use your ORM for everything - and it's why I always say "SubSonic isn't really an ORM - it's a query tool".  Given that, we want to give you a back door, and in honor of Jeff Atwood we created the Inline Query tool. Go ahead - no one's looking... do your job and be proud of it.public void Inline_Simple()  {   QueryCommand cmd = new InlineQuery().GetCommand("SELECT productID from products");   Assert.IsTrue(cmd.CommandSql 

<h2>                  "SELECT productID from products");  }    public void Inline_WithCommands()  {   QueryCommand cmd = new InlineQuery()                .GetCommand(@"SELECT productID from products                     WHERE productid=@productid", 1);     Assert.IsTrue(cmd.Parameters[0].ParameterName == "@productid");   Assert.IsTrue((int)cmd.Parameters[0].ParameterValue </h2>

 1);  }    public void Inline_AsCollection()  {   ProductCollection products =    new InlineQuery()     .ExecuteAsCollection<ProductCollection>(                           @"SELECT productID from products                             WHERE productid=@productid", 1);  }
