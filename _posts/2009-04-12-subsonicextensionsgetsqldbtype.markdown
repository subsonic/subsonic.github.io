---
layout: post
title: "SubSonic.Extensions.GetSqlDbType"
---

# SubSonic.Extensions.GetSqlDbType



<h2>Summary== Creates or opens a file for writing and writes text to it.  ==Namespace</h2>

 
  

<h2>Unit Test==public void GetSqlDbType_Should_Return_SqlType_Decimal_For_DbType_Decimal() {     var dbType = DbType.Decimal;     var sqlType = dbType.GetSqlDBType();      Assert.IsType(typeof(SqlDbType), sqlType); }  ==Source</h2>

 Sometimes it's helpful to see what's happening... 
/// <summary>         /// Returns the SqlDbType for a give DbType         /// </summary>         /// <returns></returns>         public static SqlDbType GetSqlDBType(this DbType dbType)         {             switch (dbType)             {                 case DbType.AnsiString:                     return SqlDbType.VarChar;                 case DbType.AnsiStringFixedLength:                     return SqlDbType.Char;                 case DbType.Binary:                     return SqlDbType.VarBinary;                 case DbType.Boolean:                     return SqlDbType.Bit;                 case DbType.Byte:                     return SqlDbType.TinyInt;                 case DbType.Currency:                     return SqlDbType.Money;                 case DbType.Date:                     return SqlDbType.DateTime;                 case DbType.DateTime:                     return SqlDbType.DateTime;                 case DbType.Decimal:                     return SqlDbType.Decimal;                 case DbType.Double:                     return SqlDbType.Float;                 case DbType.Guid:                     return SqlDbType.UniqueIdentifier;                 case DbType.Int16:                     return SqlDbType.Int;                 case DbType.Int32:                     return SqlDbType.Int;                 case DbType.Int64:                     return SqlDbType.BigInt;                 case DbType.Object:                     return SqlDbType.Variant;                 case DbType.SByte:                     return SqlDbType.TinyInt;                 case DbType.Single:                     return SqlDbType.Real;                 case DbType.String:                     return SqlDbType.NVarChar;                 case DbType.StringFixedLength:                     return SqlDbType.NChar;                 case DbType.Time:                     return SqlDbType.DateTime;                 case DbType.UInt16:                     return SqlDbType.Int;                 case DbType.UInt32:                     return SqlDbType.Int;                 case DbType.UInt64:                     return SqlDbType.BigInt;                 case DbType.VarNumeric:                     return SqlDbType.Decimal;                  default:                     return SqlDbType.VarChar;             }         }  

<h2>Comments</h2>

 SubSonic 3.0 implements this as an extension on System.String - 2.x uses a static method on SubSonic.Sugar.Files.
