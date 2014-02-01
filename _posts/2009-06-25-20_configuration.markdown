---
layout: post
title: "2.0 Configuration"
---

# 2.0 Configuration



<h2>Global Settings</h2>

 
defaultProvider value: string default: [Empty] When using multiple providers, this setting indicates which provider should be referenced when a provider name is not specified  
templateDirectory value: string default: [Empty] The absolute physical path to the SubSonic templates. This value is optional, and is only necessary if you are making changes to the default templates and wish to override the internal definitions. By default, the templates are located in the \SubSonic\CodeGeneration\Templates.  

<h2>Provider Level Settings</h2>

  
generatedNamespace value: string default: 'SubSonic.Generated' Sets the namespace for the generated objects and collections.  
fixPluralClassNames value: boolean default: true Indicates whether SubSonic should convert class names that it identifies as plurals to singular. For examples, Products becomes Product  
spClassName value: string default: SPs The name of the generated class that will be created to hold stored procedures (if generated). This values is ignored if extractClassNameFromSPName is enabled, and a class name can be identified from the given stored procedure name.  
useSPs value: boolean default: true Indicates whether SubSonic should generate wrappers for stored procedures in the provider database.  
stripTableText value: string default: [Empty] A comma-seperated list of values that should be stripped from table names when generating classes. The strip operation is performed using Regex.Replace(), so basic Regular Expression syntax is supported  
stripSPText value: string default: [Empty] A comma-seperated list of values that should be stripped from stored procedure names when generating classes. The strip operation is performed using Regex.Replace(), so basic Regular Expression syntax is supported  
stripViewText value: string default: [Empty] A comma-seperated list of values that should be stripped view table names when generating classes. The strip operation is performed using Regex.Replace(), so basic Regular Expression syntax is supported  
stripColumnText value: string default: [Empty] A comma-seperated list of values that should be stripped from column names when generating classes. The strip operation is performed using Regex.Replace(), so basic Regular Expression syntax is supported  
stripParamText value: string default: [Empty] A comma-seperated list of values that should be stripped from stored procedure parameter names when generating classes. The strip operation is performed using Regex.Replace(), so basic Regular Expression syntax is supported  
appendWith value: string default: X Text to append to reserved words when generating classes, so as to prevent compilation issues. For examples, for the reserved word "Type" the value would become "TypeX"  
viewStartsWith value: string default: [Empty] A value used to identify views that should be processed when SubSonic is generating classes. For example, a value of "view_" would generate classes for the view "view_Products" but not "myViewProducts"  
relatedTableLoadPrefix value: string default: [Empty] An option prefix that is applied to the methods or properties that are generate for foreign key references to tables. A common value mighy be "Get", which would generate a method such as Customer.GetProducts() instead of Customer.Products. This value can be useful for avoiding naming clashes, or to group similar methods and properties alphabetically.  
removeUnderscores value: boolean default: true Indicates whether or not SubSonic should remove underscores from database object names when generating classes.  
connectionStringName value: string default: [Empty] Indictates the name of the connection string, specified elsewhere in the configuration file, that will be used by the provider to connection to the database for all generation and persistence operations.  
regexMatchExpression value: string default: [Empty] Used in conjunction with regexReplaceExpression and regexIgnoreCase, this parameter allows for a global Regular Expression match string to specified that will be replaced by the value contained in within regexReplaceExpression.  
regexReplaceExpression value: string default: [Empty] Used in conjunction with regexMatchExpression and regexIgnorecase, this parameter specifies the global replacement value for all strings matched by regexMatchExpression.  
regexIgnoreCase value: string default: true Used in conjunction with regexMatchExpression, regexReplaceExpression, and regexDictionaryReplace, this value indicates whether or not Regular Expression operations are case sensitive.  
regexDictionaryReplace value: string default: [Empty] Allows a semicolon delimitted list of key/value pairs (comma-delimitted) for regular expression transformation operations to be specifid. This is effectively the same operation performaed by regexMatchExpression/regexReplaceExpression, but with support for multiple transformations. Syntax is as follows:  regexDictionaryReplace="Product,Widget;Customer,Client;Order,Request"  Standard regular expression terminology is supported, the value of regexIgnoreCase applies to this setting as well.  
includeTableList value: string default: * (All tables) A comma separated list of tables to be included in generation operations. If a value is set, only the tables specified will have classes generated for them  
excludeTableList value: string default: [Empty] A comma-separated list of values indicating specific tables for which classes should not be generated.  
includeProcedureList value: string default: * (All stored procedures) A comma separated list of stored procedures to be included in generation operations. If a value is set, only the tables specified will have classes generated for them  
excludeProcedureList value: string default: [Empty] A comma-separated list of values indicating specific stored procedures for which classes should not be generated.  
generateLazyLoads value: boolean default: false Indicates whether related table operations should be generated with lazy load operations. Lazy load operations can eliminate multiple database calls when reference the same record values in succession.  
generateRelatedTablesAsProperties value: boolean default: false Specifies that related table collection loading operations should be generated as properties instead of method. This is a matter of syntactical preference, as either approach will return the same results.  
extractClassNameFromSPName value: boolean default: false Specifies whether or not SubSonic should attempt to identify the destination class for generated stored procedures by parsing the store procedure name. To be placed in a non-generic class, stored procedures must follow the naming convention:  _DestinationClassName_RestOfStoredProcedureName  For the above example, SubSonic would generated a method called "RestOfStoredProcedureName" and place it in the class "DestinationClassName". Only the first match in a stored procedure is processed and must be at the beginning of the name.
