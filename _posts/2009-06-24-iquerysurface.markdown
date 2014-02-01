---
layout: post
title: "IQuerySurface"
---

# IQuerySurface



<h2>Summary== The IQuerySurface is essentially a "contract" for querying between your objects and your database and can be thought of as (basically) the DataContext in Linq to Sql.  ==The Interface</h2>

 It's pretty basic, but the interface is this:public interface IQuerySurface     {         IDataProvider Provider { get; }         Select Select { get; }         Insert Insert { get; }         SqlQuery Avg<T>(Expression<Func<T, object>> column);         SqlQuery Count<T>(Expression<Func<T, object>> column);         SqlQuery Max<T>(Expression<Func<T, object>> column);         SqlQuery Min<T>(Expression<Func<T, object>> column);         SqlQuery Variance<T>(Expression<Func<T, object>> column);         SqlQuery StandardDeviation<T>(Expression<Func<T, object>> column);         SqlQuery Sum<T>(Expression<Func<T, object>> column);         SqlQuery Delete<T>(Expression<Func<T, bool>> column) where T : new();         Query<T> GetQuery<T>();         ITable FindTable(string tableName);         Update<T> Update<T>() where T : new();     }  The 
 that you see here is SubSonic's SimpleQuery Tool.
