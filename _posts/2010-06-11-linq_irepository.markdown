---
layout: post
title: "Linq IRepository"
---

# Linq IRepository



<h2>Summary</h2>

 For testability, SubSonic 3.0 now includes an IRepository
interface that you can extend via T4 Templates. The Repository is pretty straightforward:  
public interface IRepository<T>     {         IQueryable<T> GetAll();         PagedList<T> GetPaged(Expression<Func<T, bool>> orderBy, int pageIndex, int pageSize);         IQueryable<T> Find(Expression<Func<T, bool>> expression);         void Add(T item);         int Update(T item);         int Delete(T item);         int Delete(object key);         int Delete(Expression<Func<T, bool>> expression);         T GetByKey(object key);     }  This interface is implemented in SubSonic.Core.dll.  You will find this interface as well as an implementation - SubSonicRepository
- in the SubSonic.Repository namespace.
