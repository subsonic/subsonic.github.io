---
layout: post
title: "SubSonic.Repository.SimpleRepository"
---

# SubSonic.Repository.SimpleRepository

##[Summary]()

   

<h2> Constructors </h2>

 
SimpleRepository()  SimpleRepository(String connectionStringName)  SimpleRepository(String connectionStringName, SimpleRepositoryOptions options)  SimpleRepository(SimpleRepositoryOptions options)  SimpleRepository(IDataProvider provider)  SimpleRepository(IDataProvider provider, SimpleRepositoryOptions options) 

<h2> Methods </h2>

 
Boolean Exists(T)(Expression(Func(TBoolean,Boolean)) expression)  IQueryable(T) All(T)()  SimpleRepository.T Single(T)(Expression(Func(TBoolean,Boolean)) expression)  SimpleRepository.T Single(T)(Object key)  IList(T) Find(T)(Expression(Func(TBoolean,Boolean)) expression)  PagedList(T) GetPaged(T)(Int32 pageIndex, Int32 pageSize)  PagedList(T) GetPaged(T)(String sortBy, Int32 pageIndex, Int32 pageSize)  Object Add(T)(SimpleRepository.T item)  Void AddMany(T)(IEnumerable(T) items)  Int32 Update(T)(SimpleRepository.T item)  Int32 UpdateMany(T)(IEnumerable(T) items)  Int32 Delete(T)(Object key)  Int32 DeleteMany(T)(Expression(Func(TBoolean,Boolean)) expression)  Int32 DeleteMany(T)(IEnumerable(T) items)  String ToString()  Boolean Equals(Object obj)  Int32 GetHashCode()  Type GetType()  Void Finalize()  Object MemberwiseClone() 

<h2> Examples </h2>

 Introduction to 

