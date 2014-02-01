---
layout: post
title: "Stored Procedures"
---

# Stored Procedures



<h2>Stored Procedures with 2.x== A query tool that let's you play with SPs! Quelle Chance! We know that these workhorses have a place in many applications - probably more so than many big-nose developers would care to admit.  They do what they do, and you're welcome to use them, and we won't make you feel badly.  All stored procedures are wrapped in a single class, each with the their own method. The class is by default called "SPs" and returns a type of SubSonic.StoredProcudure. So, to use your SP://for a passthrough SPs.MySPName(args...).Execute();   //returns a reader IDataReader rdr=SPs.MySPName(args).GetReader();  There's really nothing more to it than that.  ==Using Output Parameters</h2>

 If you use Output Parameters (or Return Parameters) with your stored procedures, we can try to help you. In general this is a fugly pattern but we understand, as we always say, that you know what you're doing. Even if you don't one day you will and maybe we'll all sing songs about Stored Procedures.  That said, here's how you work the Output: 
[Test] [RollBack] public void SP_Outputs() {  StoredProcedure sp = new StoredProcedure(   "SubSonicTest", DataService.GetInstance("Northwind"));  sp.Command.AddOutputParameter("@param");  sp.Execute();   //make sure there's outputs  Assert.IsTrue(sp.OutputValues.Count > 0);   //this SP just returns today's date.  //make sure it's right now!  DateTime dTest = Convert.ToDateTime(sp.OutputValues[0]);  Assert.IsTrue(dTest.Date 

<h2> DateTime.Now.Date); }  /// <summary> /// Ss the p_ outputs_ default provider. /// </summary> [Test] [RollBack] public void SP_Outputs_DefaultProvider() {  StoredProcedure sp = new StoredProcedure   ("SubSonicTestNW", DataService.GetInstance("Northwind"));  sp.Command.AddOutputParameter("@param");  sp.Execute();   //make sure there's outputs  Assert.IsTrue(sp.OutputValues.Count > 0);   //this SP just returns today's date.  //make sure it's right now!  DateTime dTest = Convert.ToDateTime(sp.OutputValues[0]);  Assert.IsTrue(dTest.Date == DateTime.Now.Date); }  ==The Quickies</h2>

 I know what you're thinking - "dude get this ornamentation outta my way. I want my data and another cofee". Thus, QuickReader:  
/// <summary> /// Ss the p_ quick reader. /// </summary> [Test] [RollBack] public void SP_QuickReader() {  int count = 0;  using(IDataReader rdr = StoredProcedure   .GetReader("CustOrderHist 'ALFKI'"))  {   while(rdr.Read())    count++;   rdr.Close();  }  Assert.IsTrue(count 

<h2> 11); }   /// <summary> /// Ss the p_ quick data set. /// </summary> [Test] [RollBack] public void SP_QuickDataSet() {  DataSet ds = StoredProcedure.GetDataSet("CustOrderHist 'ALFKI'");  Assert.IsTrue(ds.Tables[0].Rows.Count </h2>

 11); }  [Test] public void SP_Should_Execute_Without_Parameter() {  int count = 0;  using (IDataReader rdr = Northwind.SPs   .TenMostExpensiveProducts().GetReader()) {      while (rdr.Read())    count++;   rdr.Close();  }   Assert.IsTrue(count > 0); }
