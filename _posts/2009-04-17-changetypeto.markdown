---
layout: post
title: "ChangeTypeTo"
---

# ChangeTypeTo



<h2>Namespace</h2>

 
  

<h2>Summary== Changes an object's type with attention paid to nullables and generics  ==Example==DateTime newDate="12/12/09".ChangeTypeTo<DateTime>();  ==Source</h2>

 
/// <summary> /// Returns an Object with the specified Type and whose value is equivalent to the specified object. /// </summary> /// <param name="value">An Object that implements the IConvertible interface.</param> /// <returns> /// An object whose Type is conversionType (or conversionType's underlying type if conversionType /// is Nullable<>) and whose value is equivalent to value. -or- a null reference, if value is a null /// reference and conversionType is not a value type. /// </returns> /// <remarks> /// This method exists as a workaround to System.Convert.ChangeType(Object, Type) which does not handle /// nullables as of version 2.0 (2.0.50727.42) of the .NET Framework. The idea is that this method will /// be deleted once Convert.ChangeType is updated in a future version of the .NET Framework to handle /// nullable types, so we want this to behave as closely to Convert.ChangeType as possible. /// This method was written by Peter Johnson at: /// 
     {         // It's a nullable type, so instead of calling Convert.ChangeType directly which would throw a         // InvalidCastException (per 
         // determine what the underlying type is         // If it's null, it won't convert to the underlying type, but that's fine since nulls don't really         // have a type--so just return null         // Note: We only do this check if we're converting to a nullable type, since doing it outside         // would diverge from Convert.ChangeType's behavior, which throws an InvalidCastException if         // value is null and conversionType is a value type.         if (value 

<h2> null)             return null;          // It's a nullable type, and not null, so that means it can be converted to its underlying type,         // so overwrite the passed-in conversion type with this underlying type         NullableConverter nullableConverter = new NullableConverter(conversionType);         conversionType = nullableConverter.UnderlyingType;     }      // Now that we've guaranteed conversionType is something Convert.ChangeType can handle (i.e. not a     // nullable type), pass the call on to Convert.ChangeType     return Convert.ChangeType(value, conversionType); }  ==Comments</h2>

 SubSonic 3.0 implements this as an extension method - 2.x uses a static method on SubSonic.Sugar.Numeric.
