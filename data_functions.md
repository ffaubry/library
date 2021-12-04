---
title: Data Functions
description: Documentation for all Data Functions supported in Arcade.
keywords:
  - All
  - Any
  - Array
  - Attachments
  - Back
  - Boolean
  - Console
  - Count
  - Dictionary
  - Distinct
  - Domain
  - DomainCode
  - DomainName
  - Erase
  - Expects
  - Feature
  - FeatureSet
  - FeatureSetByAssociation
  - FeatureSetById
  - FeatureSetByName
  - FeatureSetByPortalItem
  - FeatureSetByRelationshipName
  - Filter
  - First
  - FromJSON
  - GdbVersion
  - GetFeatureSet
  - GetUser
  - GroupBy
  - Guid
  - Hash
  - HasKey
  - Includes
  - IndexOf
  - Insert
  - IsEmpty
  - IsNan
  - Map
  - NextSequenceValue
  - None
  - Number
  - OrderBy
  - Pop
  - Portal
  - Push
  - Reduce
  - Resize
  - Reverse
  - Schema
  - Slice
  - Sort
  - Splice
  - SubtypeCode
  - SubtypeName
  - Subtypes
  - ToHex
  - Top
  - TypeOf
---

# Data Functions

A set of convenient functions for working with and manipulating various types of data values.

---------------------

## All

### All( array, testFunction ) -> [Boolean](../../guide/types/#boolean)

**[Since version 1.16](../../guide/version-matrix)**

Indicates whether all of the elements in a given array pass a test from the provided function. Returns `true` if the function returns `true` for all items in the input array.

#### Parameters

- **`array`**: [Array](../../guide/types/#array)  
The input array to test.
- **`testFunction`**: [Function](../../guide/logic/#user-defined-functions)  
The function used to test each element in the `inputArray`. The The function must return a truthy value if the element passes the test. The function can be a user-defined function or a core Arcade function defined with the following parameter:

  - **`value`**: *  
Represents the value of an element in the array.

#### Return value: [Boolean](../../guide/types/#boolean)

`true` if the test function returns a truthy value for all the elements.

#### Example

Returns `false` because some of the elements in the input array do not pass the `isEven` test

```arcade
// isEven is used to test if each element in the array is even
// it returns true if the element is divisible by two, false if is not
function isEven(value) { return value % 2 == 0 }
// The isEven function will execute for each element in the array,
// returning the following values: false, true, false, true, false
// Since some of the values in the array did not pass the test
// (return true), the return value will be false
Any([1,2,3,4,5], isEven)
```

Uses the existing `isEmpty` Arcade function as the `testFunction`. This is valid because `isEmpty` takes a single parameter and returns a boolean value. This expression returns `true` if all of the fields are empty.

```arcade
var myArray = [ $feature.field1, $feature.field2, $feature.field3, $feature.field4];
All(myArray, isEmpty)
```


---------------------

## Any

### Any( array, testFunction ) -> [Boolean](../../guide/types/#boolean)

**[Since version 1.16](../../guide/version-matrix)**

Tests whether any of the elements in a given array pass a test from the provided function. Returns `true` if the function returns `true` for at least one item in the input array.

#### Parameters

- **`array`**: [Array](../../guide/types/#array)  
The input array to test.
- **`testFunction`**: [Function](../../guide/logic/#user-defined-functions)  
The function used to test each element in the `inputArray`. The The function must return a truthy value if the element passes the test. The function can be a user-defined function or a core Arcade function defined with the following parameter:

  - **`value`**: *  
Represents the value of an element in the array.

#### Return value: [Boolean](../../guide/types/#boolean)

`true` if the test function returns a truthy value for any of the elements.

#### Example

Returns `true` because at least one element in the input array passes the `isEven` test.

```arcade
// isEven is used to test if each element in the array is even
// it returns true if the element is divisible by two, false if is not
function isEven(value) { return value % 2 == 0 } 
// The isEven function will execute for each element in the array,
// returning the following values: false, true, false, true, false
// Since at least one value in the array passed the test
// (return true), the return value will be true
Any([1,2,3,4,5], isEven)
```

Uses the existing `isEmpty` Arcade function as the `testFunction`. This is valid because `isEmpty` takes a single parameter and returns a boolean value. This expression returns `true` if any of the fields are empty.

```arcade
var myArray = [ $feature.field1, $feature.field2, $feature.field3, $feature.field4];
Any(myArray, isEmpty)
```


---------------------

## Array

### Array( value, defaultValue? ) -> [Array](../../guide/types/#array)

**[Since version 1.12](../../guide/version-matrix)**

Returns a new array of a given length.

#### Parameters

- **`value`**: [Number](../../guide/types/#number)  
The desired length for the new array.
- **`defaultValue`** (_Optional_): *  
The value for each element in the array. If no value is specified, the default will be `null`.

#### Return value: [Array](../../guide/types/#array)

#### Example

Returns `[null, null, null, null, null]`.

```arcade
Array(5)
```

Returns `[1,1,1]`.

```arcade
Array(3, 1)
```


---------------------

## Attachments

### Attachments( feature, options? ) -> [Attachment[]](../../guide/types/#attachment)

**[Since version 1.6](../../guide/version-matrix)**

**Profiles**: [Field Calculation](../../guide/profiles/#field-calculation) | [Attribute Rules](../../guide/profiles/#attribute-rules) | [Popups](../../guide/profiles/#popups) | [Tasks](../../guide/profiles/#tasks)

Returns a list of attachments associated with the input feature. Each result includes the name of the attachment, the content type, id, and size in bytes.

#### Parameters

- **`feature`**: [Feature](../../guide/types/#feature)  
Attachments associated with this feature will be fetched from the service.
- **`options`** (_Optional_): [Dictionary](../../guide/types/#dictionary)  
Settings for the request. Dictionary properties:

  - **`types`**: [Text[]](../../guide/types/#text)  
An array of strings representing the file types to fetch. The following are supported values: `bmp, ecw, emf, eps, ps, gif, img, jp2, jpc, j2k, jpf, jpg, jpeg, jpe, png, psd, raw, sid, tif, tiff, wmf, wps, avi, mpg, mpe, mpeg, mov, wmv, aif, mid, rmi, mp2, mp3, mp4, pma, mpv2, qt, ra, ram, wav, wma, doc, docx, dot, xls, xlsx, xlt, pdf, ppt, pptx, txt, zip, 7z, gz, gtar, tar, tgz, vrml, gml, json, xml, mdb, geodatabase`
  - **`minsize`**: [Number](../../guide/types/#number)  
The minimum file size of the attachment in bytes.
  - **`maxsize`**: [Number](../../guide/types/#number)  
The maximum file size of the attachment in bytes.
  - **`metadata`** (_Optional_): [Boolean](../../guide/types/#boolean)  
Indicates whether to include attachment metadata in the function return. Only Exif metadata for images is currently supported.

#### Return value: [Attachment[]](../../guide/types/#attachment)

#### Example

Returns the number of attachments associated with the feature

```arcade
// Returns the number of attachments associated with the feature
Count(Attachments($feature))
```


---------------------

## Back

### Back( array ) -> *

**[Since version 1.12](../../guide/version-matrix)**

Returns the last element of an array. If the array is empty, then `Back(array)` will cause the script evaluation to fail.

#### Parameters

- **`array`**: [Array](../../guide/types/#array)  
The array to get the last value from.

#### Return value: *

#### Example

Returns `'gray'`.

```arcade
var colors = ['orange', 'purple', 'gray']
Back(colors)
```


---------------------

## Boolean

### Boolean( value ) -> [Boolean](../../guide/types/#boolean)

Attempts to convert the given non-boolean value to a boolean value. For example a string 'true' would become `true`.

#### Parameters

- **`value`**: [Text](../../guide/types/#text) \| [Number](../../guide/types/#number)  
A text or number value to be converted to a boolean.

#### Return value: [Boolean](../../guide/types/#boolean)

#### Example

```arcade
// returns `true`
Boolean('true')
```

```arcade
// returns `false`. A value of 1 would return `true`
Boolean(0)
```

```arcade
// returns `false`
Boolean('hello')
```


---------------------

## Console

### Console( message, [value1, ..., valueN]? ) -> Null

Logs a message in the messages window for debugging purposes. This function can be especially useful for inspecting variable values within a custom function at runtime. Unlike other functions and the `return` statement, `Console()` doesn't actually return a value; rather, it logs messages in a separate window for inspection purposes only. The successful use of this function has no computational impact on the evaluation of the expression.

#### Parameters

- **`message`**: *  
A messages to output in the messages window.
- **`[value1, ..., valueN]`** (_Optional_): *  
A list of variables, text, nunber, or dictionary to output in the messages window.

#### Return value: Null

#### Example

Prints the value of `max` for each iteration of the loop within the function

```arcade
// The messages window will log the following:
// 'current item is: 10, but max = 10'
// 'current item is: 0, but max = 10'
// 'current item is: 84, but max = 84'
// 'current item is: 30, but max = 84'

// The expression evaluates to 84
function findMax(yourArray) {
  var max = -Infinity;
  for (var i in yourArray) {
    max = IIf(yourArray[i] > max, yourArray[i], max);
    Console('current item is: ' + i + ', but max = ' + max);
  }
  return max;
}
var myArray = [ 10, 0, 84, 30];
findMax(myArray);
```


---------------------

## Count

This function has 2 signatures:

- [Count( value ) -> Number](#count1)
- [Count( features ) -> Number](#count2)

<a name="count1"></a>
### Count( value ) -> [Number](../../guide/types/#number)

Returns the number of items in an array or the number of characters in a string.

#### Parameters

- **`value`**: [Array](../../guide/types/#array) \| [Text](../../guide/types/#text)  
An array or string on which to perform the operation.

#### Return value: [Number](../../guide/types/#number)

#### Example

Returns 6

```arcade
Count([12,21,32,44,58,63])
```

Returns 13

```arcade
Count('Graham County')
```


<a name="count2"></a>
### Count( features ) -> [Number](../../guide/types/#number)

Returns the number of features in a layer.

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
A FeatureSet from which to count the number of features

#### Return value: [Number](../../guide/types/#number)

#### Example

Returns the number of features in a layer

```arcade
Count($layer)
```


---------------------

## Dictionary

This function has 2 signatures:

- [Dictionary( name1, value1, [name2, value2, ..., nameN, valueN]? ) -> Dictionary](#dictionary1)
- [Dictionary( definition ) -> Dictionary](#dictionary2)

<a name="dictionary1"></a>
### Dictionary( name1, value1, [name2, value2, ..., nameN, valueN]? ) -> [Dictionary](../../guide/types/#dictionary)

Returns a new dictionary based on the provided arguments. The arguments are name/value pairs. e.g. dictionary('field1',val,'field2',val2,...).

#### Parameters

- **`name1`**: [Text](../../guide/types/#text)  
The attribute name.
- **`value1`**: *  
The attribute value to pair to `name1`.
- **`[name2, value2, ..., nameN, valueN]`** (_Optional_): [Text](../../guide/types/#text) \| *  
Ongoing name/value pairs.

#### Return value: [Dictionary](../../guide/types/#dictionary)

#### Example

prints 3

```arcade
var d = Dictionary('field1', 1, 'field2', 2)
return d.field1 + d.field2
```


<a name="dictionary2"></a>
### Dictionary( definition ) -> [Dictionary](../../guide/types/#dictionary)

**[Since version 1.8](../../guide/version-matrix)**

Returns a new dictionary from stringified JSON.

#### Parameters

- **`definition`**: [Text](../../guide/types/#text)  
The stringified JSON to convert to an Arcade dictionary.

#### Return value: [Dictionary](../../guide/types/#dictionary)

#### Example

Creates a dictionary from stringified JSON

```arcade
var extraInfo = '{"id": 1, "population": 200, "city": "Spencer, ID"}'
var spencerIDdata = Dictionary(extraInfo)
spencerIDdata.population // Returns 200
```


---------------------

## Distinct

This function has 2 signatures:

- [Distinct( values ) -> Array](#distinct1)
- [Distinct( features, fields ) -> FeatureSet](#distinct2)

<a name="distinct1"></a>
### Distinct( values ) -> [Array](../../guide/types/#array)

**[Since version 1.1](../../guide/version-matrix)**

Returns a set of distinct, or unique, values for a given array or list of values.

#### Parameters

- **`values`**: [Array](../../guide/types/#array)  
An array of values on which to perform the operation.

#### Return value: [Array](../../guide/types/#array)

#### Example

```arcade
Distinct([1,1,2,1,1,2,2,3,4,5])
// Returns [1,2,3,4,5]
```

```arcade
Distinct('high','medium','low',0,'high','high','low')
// Returns ['high','medium','low',0]
```


<a name="distinct2"></a>
### Distinct( features, fields ) -> [FeatureSet](../../guide/types/#featureset)

**[Since version 1.8](../../guide/version-matrix)**

**Profiles**: [Attribute Rules](../../guide/profiles/#attribute-rules) | [Dashboard Data](../../guide/profiles/#dashboard-data) | [Field Calculation](../../guide/profiles/#field-calculation) | [Popups](../../guide/profiles/#popups) | [Tasks](../../guide/profiles/#tasks)

Returns a set of distinct, or unique, values from a FeatureSet.

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
A FeatureSet from which to return distinct values.
- **`fields`**: [Text](../../guide/types/#text) \| [Array](../../guide/types/#array) \| Object  
The field(s) and/or expression(s) from which to determine unique values. This parameter can be an array of field names, an array of expressions, or an object or array of objects that specify output column names where unique values will be stored. If an object is specified, the folowing specification must be used:

  - **`name`**: [Text](../../guide/types/#text)  
The name of the column to store the result of the given expression.
  - **`expression`**: [Text](../../guide/types/#text)  
A SQL-92 expression from which to calculate a unique value.

#### Return value: [FeatureSet](../../guide/types/#featureset)

#### Example

Returns a FeatureSet with a 'Status' column. Each row of the FeatureSet contains a unique stats value

```arcade
Distinct($layer, 'Status')
```

Returns a FeatureSet with a 'Status' and a 'Type' column. Each row of the FeatureSet contains a unique combination of 'Status' and 'Type' values

```arcade
Distinct($layer, ['Status', 'Type'])
```

Returns FeatureSet with a Density column with rows that may contain values of Low, High, or N/A

```arcade
Distinct($layer, {
  name: "Density",
  expression: "CASE WHEN PopDensity < 100 THEN 'Low' WHEN PopDensity >= 100 THEN 'High' ELSE 'N/A' END"
})
```

Returns FeatureSet with a Score and a Type column

```arcade
Distinct($layer, [{
  name: 'Score',
  expression: 'POPULATION_DENSITY * 0.65 + Status_Code * 0.35'
}, {
  name: 'Type',
  expression: 'Category'
}])
```


---------------------

## Domain

This function has 2 signatures:

- [Domain( feature, fieldName ) -> Dictionary](#domain1)
- [Domain( features, fieldName, subtype? ) -> Dictionary](#domain2)

<a name="domain1"></a>
### Domain( feature, fieldName ) -> [Dictionary](../../guide/types/#dictionary)

**[Since version 1.11](../../guide/version-matrix)**

Returns the domain assigned to the given field of the provided `feature`. If the `feature` belongs to a class with a subtype, this returns the domain assigned to the subtype.

#### Parameters

- **`feature`**: [Feature](../../guide/types/#feature)  
The Feature with a field that has a domain.
- **`fieldName`**: [Text](../../guide/types/#text)  
The name of the field (not the alias of the field) assigned the domain.

#### Return value: [Dictionary](../../guide/types/#dictionary)

Returns a dictionary described by the properties below.

- **`type`**: [Text](../../guide/types/#text)  
The type of domain - either `codedValue` or `range`.
- **`name`**: [Text](../../guide/types/#text)  
The domain name.
- **`dataType`**: [Text](../../guide/types/#text)  
The data type of the domain field. It can be one of the following values: `esriFieldTypeSmallInteger`, `esriFieldTypeInteger`, `esriFieldTypeSingle`, `esriFieldTypeDouble`, `esriFieldTypeString`, `esriFieldTypeDate`, `esriFieldTypeOID`, `esriFieldTypeGeometry`, `esriFieldTypeBlob`, `esriFieldTypeRaster`, `esriFieldTypeGUID`, `esriFieldTypeGlobalID`, `esriFieldTypeXML`.
- **`codedValues`**: [Dictionary[]](../../guide/types/#dictionary)  
Only applicable to `codedValue` domains. An array of dictionaries describing the valid values for the field. Each dictionary has a `code` property, which contains the actual field value, and a `name` property containing a user-friendly description of the value (e.g. `{ code: 1, name: "pavement" }`).
- **`min`**: [Number](../../guide/types/#number)  
Only applicable to `range` domains. The minimum value of the domain.
- **`max`**: [Number](../../guide/types/#number)  
Only applicable to `range` domains. The maximum value of the domain.

#### Example

The domain assigned to the feature's subtype

```arcade
var d = Domain($feature, "poleType")
// the poleType field has a coded value domain called poleTypes
// the value of d will be
// {
//   type: "codedValue" ,
//   name: "poleTypes",
//   dataType: "number",
//   codedValues: [
//     { name: "Unknown", code: 0 },
//     { name: "Wood", code: 1 },
//     { name: "Steel", code: 2 }
//   ]
// }
```


<a name="domain2"></a>
### Domain( features, fieldName, subtype? ) -> [Dictionary](../../guide/types/#dictionary)

**[Since version 1.11](../../guide/version-matrix)**

**Profiles**: [Attribute Rules](../../guide/profiles/#attribute-rules) | [Dashboard Data](../../guide/profiles/#dashboard-data) | [Popups](../../guide/profiles/#popups) | [Field Calculation](../../guide/profiles/#field-calculation) | [Tasks](../../guide/profiles/#tasks)

Returns the domain assigned to the given field of the provided `featureSet`. If the `featureSet` belongs to a class with a subtype, this returns the domain assigned to the subtype.

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
The FeatureSet whose features contain a field that has a domain.
- **`fieldName`**: [Text](../../guide/types/#text)  
The name of the field (not the alias of the field) containing the domain.
- **`subtype`** (_Optional_): [Text](../../guide/types/#text) \| [Number](../../guide/types/#number)  
The coded value for the subtype if the feature supports subtypes.

#### Return value: [Dictionary](../../guide/types/#dictionary)

Returns a dictionary described by the properties below.

- **`type`**: [Text](../../guide/types/#text)  
The type of domain - either `codedValue` or `range`.
- **`name`**: [Text](../../guide/types/#text)  
The domain name.
- **`dataType`**: [Text](../../guide/types/#text)  
The data type of the domain field. It can be one of the following values: `esriFieldTypeSmallInteger`, `esriFieldTypeInteger`, `esriFieldTypeSingle`, `esriFieldTypeDouble`, `esriFieldTypeString`, `esriFieldTypeDate`, `esriFieldTypeOID`, `esriFieldTypeGeometry`, `esriFieldTypeBlob`, `esriFieldTypeRaster`, `esriFieldTypeGUID`, `esriFieldTypeGlobalID`, `esriFieldTypeXML`.
- **`min`**: [Number](../../guide/types/#number)  
Only applicable to `range` domains. The minimum value of the domain.
- **`max`**: [Number](../../guide/types/#number)  
Only applicable to `range` domains. The maximum value of the domain.
- **`codedValues`**: [Dictionary[]](../../guide/types/#dictionary)  
Only applicable to `codedValue` domains. An array of dictionaries describing the valid values for the field. Each dictionary has a `code` property, which contains the actual field value, and a `name` property containing a user-friendly description of the value (e.g. `{ code: 1, name: "pavement" }`).

#### Example

The domain assigned to the feature's subtype

```arcade
var fsPole = FeatureSetByName($layer, "Pole", 1);
var d = Domain(fsPole, "poleType")
// the poleType field has a coded value domain called poleTypes
// the value of d will be
// {
//   type: "codedValue" ,
//   name: "poleTypesThreePhase",
//   dataType: "number",
//   codedValues: [
//     { name: "Unknown", code: 0 },
//     { name: "Wood", code: 1 },
//     { name: "Steel", code: 2 }
//     { name: "Reinforced Steel", code: 3 }
//   ]
// }
```


---------------------

## DomainCode

This function has 2 signatures:

- [DomainCode( feature, fieldName, value?, subtype? ) -> Text](#domaincode1)
- [DomainCode( features, fieldName, value, subtype? ) -> Text](#domaincode2)

<a name="domaincode1"></a>
### DomainCode( feature, fieldName, value?, subtype? ) -> [Text](../../guide/types/#text)

**[Since version 1.7](../../guide/version-matrix)**

Returns the code of an associated domain description in a feature.

#### Parameters

- **`feature`**: [Feature](../../guide/types/#feature)  
The feature with a field that has a domain.
- **`fieldName`**: [Text](../../guide/types/#text)  
The name of the field (not the alias of the field) containing the domain.
- **`value`** (_Optional_): [Text](../../guide/types/#text)  
The value to be converted back into a code.
- **`subtype`** (_Optional_): [Text](../../guide/types/#text)  
The coded number for the subtype if the feature supports subtyping. If not provided, the current feature's subtype (if it has one), will be used.

#### Return value: [Text](../../guide/types/#text)

#### Example

prints the domain description for the field referenced.

```arcade
DomainCode($feature, 'Enabled', 'True')
```


<a name="domaincode2"></a>
### DomainCode( features, fieldName, value, subtype? ) -> [Text](../../guide/types/#text)

**[Since version 1.7](../../guide/version-matrix)**

Returns the code of an associated domain description in a feature set.

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
The feature set with a field that has a domain.
- **`fieldName`**: [Text](../../guide/types/#text)  
The name of the field (not the alias of the field) containing the domain.
- **`value`**: [Text](../../guide/types/#text)  
The value to be converted back into a code. The returned code comes from the service metadata.
- **`subtype`** (_Optional_): [Text](../../guide/types/#text)  
The coded number for the subtype if the feature set supports subtyping.

#### Return value: [Text](../../guide/types/#text)

#### Example

prints the domain description for the field referenced.

```arcade
DomainCode($layer, 'Enabled', 'True', subtype)
```


---------------------

## DomainName

This function has 2 signatures:

- [DomainName( feature, fieldName, code?, subtype? ) -> Text](#domainname1)
- [DomainName( features, fieldName, code?, subtype? ) -> Text](#domainname2)

<a name="domainname1"></a>
### DomainName( feature, fieldName, code?, subtype? ) -> [Text](../../guide/types/#text)

**[Since version 1.7](../../guide/version-matrix)**

Returns the descriptive name for a domain code in a feature.

#### Parameters

- **`feature`**: [Feature](../../guide/types/#feature)  
The feature with a field that has a domain.
- **`fieldName`**: [Text](../../guide/types/#text)  
The name of the field (not the alias of the field) containing the domain.
- **`code`** (_Optional_): [Text](../../guide/types/#text)  
The code associated with the desired descriptive name. If not provided, the field value in the feature will be returned.
- **`subtype`** (_Optional_): [Text](../../guide/types/#text)  
The coded number of the subtype if the feature supports subtyping. If not provided, the feature's subtype (if it has one) will be used.

#### Return value: [Text](../../guide/types/#text)

#### Example

prints the domain description for the referenced field

```arcade
DomainName($feature, 'fieldName')
```


<a name="domainname2"></a>
### DomainName( features, fieldName, code?, subtype? ) -> [Text](../../guide/types/#text)

**[Since version 1.7](../../guide/version-matrix)**

Returns the descriptive name for a domain code in a feature.

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
A FeatureSet with a field that has a domain.
- **`fieldName`**: [Text](../../guide/types/#text)  
The name of the field (not the alias of the field) containing the domain.
- **`code`** (_Optional_): [Text](../../guide/types/#text)  
The code associated with the desired descriptive name. The returned code comes from the service metadata.
- **`subtype`** (_Optional_): [Text](../../guide/types/#text)  
The coded number of the subtype if the FeatureSet supports subtyping.

#### Return value: [Text](../../guide/types/#text)

#### Example

prints the domain description for the referenced field

```arcade
DomainName($layer, 'fieldName')
```


---------------------

## Erase

### Erase( array, index ) -> Null

**[Since version 1.12](../../guide/version-matrix)**

Removes a value from an array at a given index. Existing elements positioned at or above the given index will shift down one index value. The array decreases in size by one.

#### Parameters

- **`array`**: [Array](../../guide/types/#array)  
The array to remove the value from.
- **`index`**: [Number](../../guide/types/#number)  
The index of the value to remove from the array. If a negative index is provided, it will be used as an offset from the end of the array.

#### Example

```arcade
var colors = ['orange', 'purple', 'gray']
Erase(colors, 1)
// colors = ['orange','gray']
```

```arcade
var colors = ['orange', 'purple', 'gray']
Erase(colors, -1)
// colors = ['orange','purple']
```


---------------------

## Expects

This function has 2 signatures:

- [Expects( feature, field1, [field2, ..., fieldN]? ) -> Null](#expects1)
- [Expects( features, field1, [field2, ..., fieldN]? ) -> Null](#expects2)

<a name="expects1"></a>
### Expects( feature, field1, [field2, ..., fieldN]? ) -> Null

**[Since version 1.15](../../guide/version-matrix)**

Requests additional attributes for the given feature. In some profiles, such as Visualization and Labeling, apps only request the data attributes required for rendering each feature or label. Some expressions dynamically reference field names with variables rather than string literals. This makes it hard for rendering and labeling engines to detect fields required for rendering. This function allows you to explicitly indicate required fields as a list. You can also request all or a subset of fields using a wildcard. Because expressions execute on a per feature basis, the wildcard should be used with caution, especially in layers containing many features. Requesting too much data can result in very poor app performance.

#### Parameters

- **`feature`**: [Feature](../../guide/types/#feature)  
The feature to which the requested fields will be attached.
- **`field1`**: [Text](../../guide/types/#text)  
A field name to request for the given feature. List only fields required for use in the expression. If necessary, you can request all fields using the wildcard `*` character. However, this should be avoided to prevent loading an unnecessary amount of data that can negatively impact app performance.
- **`[field2, ..., fieldN]`** (_Optional_): [Text](../../guide/types/#text)  
An ongoing list of field names to request for the given feature. List only fields required for use in the expression.

#### Return value: Null

#### Example

Requests fields not easily detected by the renderer

```arcade
// Request multiple years of population data if the
// fields cannot be easily detected by the renderer or labels
Expects($feature, 'POP_2020', 'POP_2010')
var thisYear = 2020;
var lastDecade = thisYear - 10;
return $feature['POP_'+thisYear] - $feature['POP_'+lastDecade]
```

Requests all data matching a pattern in the field name

```arcade
// Request all the data beginning with 'POP'. This is
// necessary because the renderer can't easily detect
// the required fields based on this expression
Expects($feature, 'POP*')

var startYear = 1880;
var endYear = 2020;
var changes = [];

for(var y=startYear; y<endYear; y+=10){
  var startPop = $feature['POP_' + y];
  var endPop = $feature['POP_' + (y+10)];
  var change = endPop - startPop;
  Push(changes, change);
}
Max(changes);
```

Requests all data for the feature

```arcade
// Request all fields because the required fields may
// be based on unknown information like a relative date
Expects($feature, '*')

var casesToday = $feature[ 'CASES_' + Text(d, 'MM_DD_Y') ];
var casesYesterday = $feature[ 'CASES_' + Text(DateAdd( Today(), -1, 'days', 'MM_DD_Y') ];
// Change in cases from yesterday
return casesToday - casesYesterday;
```


<a name="expects2"></a>
### Expects( features, field1, [field2, ..., fieldN]? ) -> Null

**[Since version 1.15](../../guide/version-matrix)**

Requests additional attributes for the given FeatureSet.

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
The feature set to which the requested fields will be attached.
- **`field1`**: [Text](../../guide/types/#text)  
A field name to request for the given feature. List only fields required for use in the expression. If necessary, you can request all fields using the wildcard `*` character. However, this should be avoided to prevent loading an unnecessary amount of data that can negatively impact app performance.
- **`[field2, ..., fieldN]`** (_Optional_): [Text](../../guide/types/#text)  
An ongoing list of field names to request for the given feature. List only fields required for use in the expression.

#### Return value: Null

#### Example

Requests the POPULATION field for the features in the cluster

```arcade
// If the layer is clustered based on count,
// only the OBJECTID field is requested by default.
// To display the sum of the POPULATION field
// for all features in the cluster, we must
// explicitly request the POPULATION data. 
Expects($aggregatedFeatures, 'POPULATION')
Text(Sum($aggregatedFeatures, 'POPULATION'), '#,###')
```


---------------------

## Feature

### Feature( featureGeometry, attribute1, value1, [attribute2, value2, ..., attributeN, valueN]? ) -> [Feature](../../guide/types/#feature)

Creates a new feature. Alternatively, it can be called with object notation: `Feature({geometry: {}, attributes: {...}})` or with two parameters: `Feature(geometry, attributes);`.

#### Parameters

- **`featureGeometry`**: [Geometry](../../guide/types/#geometry)  
The geometry of the feature.
- **`attribute1`**: [Text](../../guide/types/#text)  
The first attribute's name.
- **`value1`**: [Text](../../guide/types/#text) \| [Date](../../guide/types/#date) \| [Number](../../guide/types/#number) \| [Boolean](../../guide/types/#boolean)  
The first attribute's value.
- **`[attribute2, value2, ..., attributeN, valueN]`** (_Optional_): *  
Ongoing name/value pairs for each attribute in the feature.

#### Return value: [Feature](../../guide/types/#feature)

#### Example

```arcade
Feature(pointGeometry, 'city_name', 'Spokane', 'population', 210721)
```

###### Create a feature from another feature.
```arcade
var dict = { hello:10 }
var p = point({x:10, y:20, spatialReference:{wkid:102100}})
var ftr1 = Feature(p,dict)
var ftr2 = Feature(ftr1)
```

###### Create a feature from a JSON string.
```arcade
var JSONString = "{'geometry':{'x':10,'y':20,'spatialReference':{'wkid':102100}},'attributes':{'hello':10}}"
Feature(JSONString)
```


---------------------

## FeatureSet

### FeatureSet( definition ) -> [FeatureSet](../../guide/types/#featureset)

**[Since version 1.5](../../guide/version-matrix)**

**Profiles**: [Attribute Rules](../../guide/profiles/#attribute-rules) | [Dashboard Data](../../guide/profiles/#dashboard-data) | [Popups](../../guide/profiles/#popups) | [Field Calculation](../../guide/profiles/#field-calculation) | [Tasks](../../guide/profiles/#tasks)

Creates a new FeatureSet from JSON according to the ArcGIS REST spec. See the snippet below for an example of this.

#### Parameters

- **`definition`**: [Text](../../guide/types/#text)  
The JSON describing a set of features. The JSON must be contained in a text value.

#### Return value: [FeatureSet](../../guide/types/#featureset)

#### Example

###### Create a FeatureSet from JSON.
```arcade
// JSON representation of the feature used in the snippet below
// {
//   'fields': [{
//     'alias': 'RANK',
//     'name': 'RANK',
//     'type': 'esriFieldTypeInteger'
//   }, {
//     'alias': 'ELEV_m',
//     'name': 'ELEV_m',
//     'type': 'esriFieldTypeInteger'
//   }],
//   'spatialReference': { 'wkid': 4326 },
//   'geometryType': 'esriGeometryPoint',
//   'features': [{
//     'geometry': {
//       'spatialReference': { 'wkid': 4326 },
//       'x': -151.0063,
//       'y': 63.069
//     },
//     'attributes': {
//       'RANK': 1,
//       'ELEV_m': 6168
//     }
//   }]
// };
// The Dictionary representation of the FeatureSet must be a stringified object
var features = FeatureSet('{"fields":[{"alias":"RANK","name":"RANK","type":"esriFieldTypeInteger"},{"alias":"ELEV_m","name":"ELEV_m","type":"esriFieldTypeInteger"}],"spatialReference":{"wkid":4326},"geometryType":"esriGeometryPoint","features":[{"geometry":{"spatialReference":{"wkid":4326},"x":-151.0063,"y":63.069},"attributes":{"RANK":1,"ELEV_m":6168}}]}')
```


---------------------

## FeatureSetByAssociation

### FeatureSetByAssociation( feature, associationType, terminalName? ) -> [FeatureSet](../../guide/types/#featureset)

**[Since version 1.9](../../guide/version-matrix)**

**Profiles**: [Attribute Rules](../../guide/profiles/#attribute-rules) | [Dashboard Data](../../guide/profiles/#dashboard-data) | [Popups](../../guide/profiles/#popups) | [Tasks](../../guide/profiles/#tasks)

Returns all the features associated with the input feature as a FeatureSet. This is specific to Utility Network workflows.

#### Parameters

- **`feature`**: [Feature](../../guide/types/#feature)  
The feature from which to query for all associated features. This feature must be coming from a feature service; feature collections are not supported.
- **`associationType`**: [Text](../../guide/types/#text)  
The type of association with the feature to be returned.

 **Possible Values:** `connected` \| `container` \| `content` \| `structure` \| `attached`  
 Added at 1.10: `junctionEdge` \| `midspan`
- **`terminalName`** (_Optional_): [Text](../../guide/types/#text)  
Only applicable to `connected` association types.

#### Return value: [FeatureSet](../../guide/types/#featureset)

Returns a FeatureSet containing features with the field specification described in the table below.

- **`className`**: [Text](../../guide/types/#text)  
The class name based on the value of `TONETWORKSOURCEID` or `FROMNETWORKSOURCEID`.
- **`globalId`**: [Text](../../guide/types/#text)  
The Global ID of the feature in the other table (i.e. either the value of `TOGLOBALID` or `FROMGLOBALID`).
- **`isContentVisible`**: [Number](../../guide/types/#number)  
Can either be a value of `1` (visible) or `0` (not visible). This value represents the visibility of the associated content and is only applicable for containment associations.
- **`objectId`**: [Text](../../guide/types/#text)  
The ObjectID of the row in the association table.
- **`percentAlong`**: [Number](../../guide/types/#number)  
Applies to `midspan` association types. Returns a floating point number from 0-1 indicating the location (as a ratio) of the junction along the edge.
- **`side`**: [Text](../../guide/types/#text)  
Applies to `junctionEdge` association types. Indicates which side the junction is on.

 **Possible values:** `from` \| `to`

#### Example

###### Returns all assets that have connectivity associations with the low side terminal of the transformer.
```arcade
FeatureSetByAssociation($feature, 'connected', 'Low');
```

###### Returns the number of electric devices associated with the feature
```arcade
var allContent = FeatureSetByAssociation ($feature, "content");
var devicesRows = Filter(allContent, "className = 'Electric Device'");
var devicesCount = Count(devicesRows);
return devicesCount;
```


---------------------

## FeatureSetById

### FeatureSetById( featureSetCollection, id, fields?, includeGeometry? ) -> [FeatureSet](../../guide/types/#featureset)

**[Since version 1.5](../../guide/version-matrix)**

**Profiles**: [Attribute Rules](../../guide/profiles/#attribute-rules) | [Dashboard Data](../../guide/profiles/#dashboard-data) | [Popups](../../guide/profiles/#popups) | [Field Calculation](../../guide/profiles/#field-calculation) | [Tasks](../../guide/profiles/#tasks)

Creates a FeatureSet from a Feature Layer based on its layer ID within a map or feature service. Limiting the number of fields in the request and excluding the geometry can improve the performance of the script.

#### Parameters

- **`featureSetCollection`**: [FeatureSetCollection](../../guide/types/#featuresetcollection)  
The map or feature service containing one or more layers from which to create a FeatureSet. Typically, this value is the `$map` or `$datastore` global.
- **`id`**: [Text](../../guide/types/#text)  
The ID of the layer within the given `map`. This layer must be created from a feature service; feature collections are not supported. **Please note that this must be a string literal.**
- **`fields`** (_Optional_): [Text[]](../../guide/types/#text)  
The fields to include in the FeatureSet. By default, all fields are included. To request all fields in the layer, set this value to `['*']`. Limiting the number of fields improves the performance of the script.
- **`includeGeometry`** (_Optional_): [Boolean](../../guide/types/#boolean)  
Indicates whether to include the geometry in the features. By default, this is `true`. For performance reasons, you should only request the geometry if necessary, such as for use in geometry functions.

#### Return value: [FeatureSet](../../guide/types/#featureset)

#### Example

###### Returns the number of features in the layer with the id DemoLayerWM_1117 in the given map.
```arcade
var features = FeatureSetById($map,'DemoLayerWM_1117', ['*'], true);
Count( features );
```


---------------------

## FeatureSetByName

### FeatureSetByName( featureSetCollection, title, fields?, includeGeometry? ) -> [FeatureSet](../../guide/types/#featureset)

**[Since version 1.5](../../guide/version-matrix)**

**Profiles**: [Attribute Rules](../../guide/profiles/#attribute-rules) | [Dashboard Data](../../guide/profiles/#dashboard-data) | [Popups](../../guide/profiles/#popups) | [Field Calculation](../../guide/profiles/#field-calculation) | [Tasks](../../guide/profiles/#tasks)

Creates a FeatureSet from a Feature Layer based on its name within a map or feature service. Keep in mind this name is not necessarily unique. It is therefore more appropriate to create a FeatureSet using `FeatureSetById()`. Limiting the number of fields in the FeatureSet and excluding the geometry can improve the performance of the script.

#### Parameters

- **`featureSetCollection`**: [FeatureSetCollection](../../guide/types/#featuresetcollection)  
The map or feature service containing one or more layers from which to create a FeatureSet. Typically, this value is the `$map` or `$datastore` global.
- **`title`**: [Text](../../guide/types/#text)  
The title of the layer within the given `map`. This layer must be created from a feature service; feature collections are not supported. **Please note that this must be a string literal.**
- **`fields`** (_Optional_): [Text[]](../../guide/types/#text)  
The fields to include in the FeatureSet. By default, all fields are included. To request all fields in the layer, set this value to `['*']`. Limiting the number of fields improves the performance of the script.
- **`includeGeometry`** (_Optional_): [Boolean](../../guide/types/#boolean)  
Indicates whether to include the geometry in the features. By default, this is `true`. For performance reasons, you should only request the geometry if necessary, such as for use in geometry functions.

#### Return value: [FeatureSet](../../guide/types/#featureset)

#### Example

###### Returns the number of features in the layer with the title 'Bike routes' in the given map.
```arcade
var features = FeatureSetByName($map,'Bike routes', ['*'], true);
Count(features);
```


---------------------

## FeatureSetByPortalItem

### FeatureSetByPortalItem( portalObject, itemId, layerId, fields?, includeGeometry? ) -> [FeatureSet](../../guide/types/#featureset)

**[Since version 1.8](../../guide/version-matrix)**

**Profiles**: [Dashboard Data](../../guide/profiles/#dashboard-data) | [Field Calculation](../../guide/profiles/#field-calculation) | [Popups](../../guide/profiles/#popups) | [Tasks](../../guide/profiles/#tasks)

Creates a FeatureSet from a Feature Layer in a portal item from a given Portal. Limiting the number of fields in the FeatureSet and excluding the geometry can improve the performance of the script.

#### Parameters

- **`portalObject`**: [Portal](../../guide/types/#portal)  
The Portal from which to query features from a given portal item ID.
- **`itemId`**: [Text](../../guide/types/#text)  
The GUID of the portal item referencing a feature layer or feature service. *Please note that this must be a string literal.
- **`layerId`**: [Number](../../guide/types/#number)  
The ID of the layer in the feature service. This layer must be created from a feature service; feature collections are not supported.
- **`fields`** (_Optional_): [Text[]](../../guide/types/#text)  
The fields to include in the FeatureSet. By default, all fields are included. To request all fields in the layer, set this value to `['*']`. Limiting the number of fields improves the performance of the script.
- **`includeGeometry`** (_Optional_): [Boolean](../../guide/types/#boolean)  
Indicates whether to include the geometry in the features. For performance reasons, you should only request the geometry if necessary, such as for use in geometry functions.

#### Return value: [FeatureSet](../../guide/types/#featureset)

#### Example

###### Returns the number of features in the layer from a different portal than the feature in the map
```arcade
var features = FeatureSetByPortalItem(
  Portal('https://www.arcgis.com'),
  '7b1fb95ab77f40bf8aa09c8b59045449',
  0,
  ['Name', 'Count'],
  false
);
Count(features);
```


---------------------

## FeatureSetByRelationshipName

### FeatureSetByRelationshipName( feature, relationshipName, fieldNames?, includeGeometry? ) -> [FeatureSet](../../guide/types/#featureset)

**[Since version 1.8](../../guide/version-matrix)**

**Profiles**: [Attribute Rules](../../guide/profiles/#attribute-rules) | [Dashboard Data](../../guide/profiles/#dashboard-data) | [Field Calculation](../../guide/profiles/#field-calculation) | [Popups](../../guide/profiles/#popups) | [Tasks](../../guide/profiles/#tasks)

Returns the related records for a given feature as a FeatureSet.

#### Parameters

- **`feature`**: [Feature](../../guide/types/#feature)  
The feature from which to fetch related records. This feature must be coming from a feature service; feature collections are not supported.
- **`relationshipName`**: [Text](../../guide/types/#text)  
The name of the relationship according to the feature service associated with the given feature.
- **`fieldNames`** (_Optional_): [Text[]](../../guide/types/#text)  
The fields to return in the FeatureSet. This list includes fields from both the relationship table and the input Feature.
- **`includeGeometry`** (_Optional_): [Boolean](../../guide/types/#boolean)  
Indicates whether to return the geometry for the resulting features.

#### Return value: [FeatureSet](../../guide/types/#featureset)

#### Example

###### Returns the sum of several fields across all related records
```arcade
var results = FeatureSetByRelationshipName($feature, 'Election_Results', ['*'], false)
Sum(results, 'democrat + republican + other')
```


---------------------

## Filter

This function has 2 signatures:

- [Filter( features, sqlExpression ) -> FeatureSet](#filter1)
- [Filter( array, filterFunction ) -> Array](#filter2)

<a name="filter1"></a>
### Filter( features, sqlExpression ) -> [FeatureSet](../../guide/types/#featureset)

**[Since version 1.5](../../guide/version-matrix)**

**Profiles**: [Attribute Rules](../../guide/profiles/#attribute-rules) | [Dashboard Data](../../guide/profiles/#dashboard-data) | [Popups](../../guide/profiles/#popups) | [Field Calculation](../../guide/profiles/#field-calculation) | [Tasks](../../guide/profiles/#tasks)

Creates a new FeatureSet with all the features that pass the SQL92 expression filter.

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
The FeatureSet, or layer, to filter.
- **`sqlExpression`**: [Text](../../guide/types/#text)  
The SQL92 expression used to filter features in the layer. This expression can substitute an Arcade variable using the `@` character. See the snippet below for an example.

#### Return value: [FeatureSet](../../guide/types/#featureset)

#### Example

###### Filter features using a SQL92 expression
```arcade
// Returns all features with a Population greater than 10,000
var result = Filter($layer, 'POPULATION > 10000');
```

###### Filter features using a SQL92 expression with a variable substitute
```arcade
// Returns all features with a Population greater than the dataset average
var averageValue = Average($layer, 'POPULATION')
var result = Filter($layer, 'POPULATION > @averageValue');
```


<a name="filter2"></a>
### Filter( array, filterFunction ) -> [Array](../../guide/types/#array)

**[Since version 1.16](../../guide/version-matrix)**

Creates a new array with the elements filtered from the input array that pass a test from the provided function.

#### Parameters

- **`array`**: [Array](../../guide/types/#array)  
The input array to filter.
- **`filterFunction`**: [Function](../../guide/logic/#user-defined-functions)  
The function used to filter elements in the array. This must be a user-defined function or a core Arcade function defined with the following parameters:

 **Parameters**  
 `value`: Represents the value of an element in the array.

 **Return value**  
 The function must return either `true` or `false` indicating whether to include a value in the output array.

#### Return value: [Array](../../guide/types/#array)

#### Example

Returns a new array comprised of elements that passed the `isEven` filter.

```arcade
function isEven(i) { return i % 2 == 0 } 
Filter([1,2,3,4,5], isEven) // Returns [2,4]
// Since 2 and 4 are even, they are the only values
// included in the output array.
```

Uses the existing `isEmpty` Arcade function in the `filterFunction`. Returns a new array of fields that are not empty.

```arcade
var myArray = [ $feature.field1, $feature.field2, $feature.field3, $feature.field4];

function isNotEmpty(value){
  return !isEmpty(value);
}
Filter(myArray, isNotEmpty)
// Returns only values that are defined,
// excluding empty values from the result
```


---------------------

## First

This function has 2 signatures:

- [First( array ) -> *](#first1)
- [First( features ) -> Feature](#first2)

<a name="first1"></a>
### First( array ) -> *

Returns the first element in an array. Returns `null` if the array is empty.

#### Parameters

- **`array`**: [Array](../../guide/types/#array)  
The array from which to return the first item.

#### Return value: *

#### Example

prints 'orange'

```arcade
First(['orange', 'purple', 'gray'])
```


<a name="first2"></a>
### First( features ) -> [Feature](../../guide/types/#feature)

Returns the first feature in a FeatureSet. Returns `null` if the FeatureSet is empty.

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
The FeatureSet from which to return the first feature.

#### Return value: [Feature](../../guide/types/#feature)

#### Example

returns the area of the first feature in the layer.

```arcade
Area( First($layer) )
```


---------------------

## FromJSON

### FromJSON( jsonText ) -> [Dictionary](../../guide/types/#dictionary) \| [Array](../../guide/types/#array) \| [Text](../../guide/types/#text) \| [Boolean](../../guide/types/#boolean) \| [Number](../../guide/types/#number)

**[Since version 1.14](../../guide/version-matrix)**

Converts stringified (serialized) JSON objects into their equivalent Arcade data types.

#### Parameters

- **`jsonText`**: [Text](../../guide/types/#text)  
The stringified JSON to deserialize to an Arcade data type.

#### Return value: [Dictionary](../../guide/types/#dictionary) \| [Array](../../guide/types/#array) \| [Text](../../guide/types/#text) \| [Boolean](../../guide/types/#boolean) \| [Number](../../guide/types/#number)

#### Example

Converts text to a boolean

```arcade
FromJSON("true")
// Returns true
```

Converts text to a number

```arcade
fromJSON("731.1")
// returns 731.1
```

Converts text to a dictionary

```arcade
var d = fromJSON('{"kids": 3, "adults": 4 }')
d.kids + d.adults
// returns 7
```

Converts text to an array

```arcade
fromJSON('["one", 2, "three", false]')
// returns [ "one", 2, "three", false ]
```

Converts text to null

```arcade
fromJSON("null")
// returns null
```


---------------------

## GdbVersion

This function has 2 signatures:

- [GdbVersion( feature ) -> Text](#gdbversion1)
- [GdbVersion( features ) -> Text](#gdbversion2)

<a name="gdbversion1"></a>
### GdbVersion( feature ) -> [Text](../../guide/types/#text)

**[Since version 1.12](../../guide/version-matrix)**

Returns the name of the current geodatabase version for branch or versioned data. When the data is not in a multi-user geodatabase, an empty string will be returned. See [Overview of Versioning](https://pro.arcgis.com/en/pro-app/help/data/geodatabases/overview/overview-of-versioning-in-arcgis-pro.htm) for more information.

#### Parameters

- **`feature`**: [Feature](../../guide/types/#feature)  
A Feature from which to return the current geodatabase version of the associated layer.

#### Return value: [Text](../../guide/types/#text)

#### Example

Returns the geodatabase version of the given feature

```arcade
GdbVersion($feature)
```


<a name="gdbversion2"></a>
### GdbVersion( features ) -> [Text](../../guide/types/#text)

**[Since version 1.12](../../guide/version-matrix)**

Returns the name of the current geodatabase version for branch or versioned data. When the data is not in a multi-user geodatabase, an empty string will be returned. See [Overview of Versioning](https://pro.arcgis.com/en/pro-app/help/data/geodatabases/overview/overview-of-versioning-in-arcgis-pro.htm) for more information.

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
A FeatureSet from which to return the current geodatabase version.

#### Return value: [Text](../../guide/types/#text)

#### Example

Returns the geodatabase version of the given FeatureSet

```arcade
GdbVersion($layer)
```


---------------------

## GetFeatureSet

### GetFeatureSet( feature, source? ) -> [FeatureSet](../../guide/types/#featureset)

**[Since version 1.14](../../guide/version-matrix)**

**Profiles**: [Attribute Rules](../../guide/profiles/#attribute-rules) | [Dashboard Data](../../guide/profiles/#dashboard-data) | [Popups](../../guide/profiles/#popups) | [Field Calculation](../../guide/profiles/#field-calculation) | [Tasks](../../guide/profiles/#tasks)

Gets the FeatureSet in which the input feature belongs. The returned FeatureSet represents all features from the input feature's parent/root layer or table.

#### Parameters

- **`feature`**: [Feature](../../guide/types/#feature)  
The feature belonging to a parent or root FeatureSet.
- **`source`** (_Optional_): [Text](../../guide/types/#text)  
Indicates the source FeatureSet to return.

 **Possible Values:**  
 - `datasource` - (default) Returns all the features from the input feature's data source without any filters or definition expressions as a FeatureSet. - `root` - Returns the initial FeatureSet to which the input feature belongs. This may be a filtered subset of all the features in the data source. - `parent` - Returns the parent FeatureSet of the input feature. This can be a smaller set of features than the original data source or root FeatureSet.

#### Return value: [FeatureSet](../../guide/types/#featureset)

#### Example

###### Returns a FeatureSet representing all the features in the data source.
```arcade
// The data source for the 'Bike routes' layer has 2,000 features. 
// The map sets a definition expression on the 'Bike routes' layer and filters it to 100 features.
var fs1 = FeatureSetByName($map, 'Bike routes', ['*'], true);
var fs2 = top(fs1, 10) 
var f = First(fs2)
GetFeatureSet(f)
// returns a FeatureSet representing the data source with 2,000 features
```

###### Returns the root FeatureSet of the feature.
```arcade
// The data source for the 'Bike routes' layer has 2,000 features. 
// The map sets a definition expression on the 'Bike routes' layer and filters it to 100 features.
var fs1 = FeatureSetByName($map, 'Bike routes', ['*'], true);
var fs2 = top(fs1, 10) 
var f = First(fs2)
GetFeatureSet(f, 'root')
// returns the root FeatureSet representing 100 features
```

###### Returns the parent FeatureSet of the feature.
```arcade
// The data source for the 'Bike routes' layer has 2,000 features. 
// The map sets a definition expression on the 'Bike routes' layer and filters it to 100 features.
var fs1 = FeatureSetByName($map, 'Bike routes', ['*'], true);
var fs2 = top(fs1, 10) 
var f = First(fs2)
GetFeatureSet(f, 'parent')
// returns the parent FeatureSet representing 10 features
```

###### Returns the number of features in the data source table within 1 mile of the feature.
```arcade
var fullFeatureSet = GetFeatureSet($feature);
var featuresOneMile = Intersects(fullFeatureSet, BufferGeodetic($feature, 1, 'miles'))
Count(featuresOneMile)
```


---------------------

## GetUser

This function has 4 signatures:

- [GetUser( portalObject, username? ) -> Dictionary](#getuser1)
- [GetUser( features, username? ) -> Dictionary](#getuser2)
- [GetUser( portalObject, extensions? ) -> Dictionary](#getuser3)
- [GetUser( features, extensions? ) -> Dictionary](#getuser4)

<a name="getuser1"></a>
### GetUser( portalObject, username? ) -> [Dictionary](../../guide/types/#dictionary)

**[Since version 1.12](../../guide/version-matrix)**

**Profiles**: [Attribute Rules](../../guide/profiles/#attribute-rules) | [Dashboard Data](../../guide/profiles/#dashboard-data) | [Popups](../../guide/profiles/#popups) | [Field Calculation](../../guide/profiles/#field-calculation) | [Tasks](../../guide/profiles/#tasks)

Returns the current user from the workspace. For data from a service, either the Portal user or Server user is returned. For data from a database connection, the database user is returned. When no user is associated with the workspace, such as a file geodatabase, an empty string will be returned.

#### Parameters

- **`portalObject`**: [Portal](../../guide/types/#portal)  
A Portal from which to return the current user.
- **`username`** (_Optional_): [Text](../../guide/types/#text)  
The username of the user you want to return. Only limited information will be returned based on your permissions when making the request.

#### Return value: [Dictionary](../../guide/types/#dictionary)

Returns a dictionary described by the properties below.

- **`email`**: [Text](../../guide/types/#text)  
The email address associated with the user's account.
- **`fullName`**: [Text](../../guide/types/#text)  
The user's first and last name.
- **`groups`**: [Text[]](../../guide/types/#text)  
An array of groups that the user belongs to.
- **`id`**: [Text](../../guide/types/#text)  
The user id of the returned user.
- **`privileges`**: [Text[]](../../guide/types/#text)  
An array of privileges that the user has within their organization (e.g. edit, view, etc).
- **`role`**: [Text](../../guide/types/#text)  
The role that the user plays within their organization (e.g. Administrator, Publisher, User, Viewer, or Custom).
- **`username`**: [Text](../../guide/types/#text)  
The username of the returned user.

#### Example

Returns the dictionary for the user currently logged in based on the workspace connection from the given portal.

```arcade
GetUser(Portal('https://www.arcgis.com'))
```


<a name="getuser2"></a>
### GetUser( features, username? ) -> [Dictionary](../../guide/types/#dictionary)

**[Since version 1.12](../../guide/version-matrix)**

**Profiles**: [Attribute Rules](../../guide/profiles/#attribute-rules) | [Dashboard Data](../../guide/profiles/#dashboard-data) | [Popups](../../guide/profiles/#popups) | [Field Calculation](../../guide/profiles/#field-calculation) | [Tasks](../../guide/profiles/#tasks)

Returns the current user from the workspace. For data from a service, either the Portal user or Server user is returned. For data from a database connection, the database user is returned. When no user is associated with the workspace, such as a file geodatabase, an empty string will be returned.

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
A FeatureSet from which to return the current user.
- **`username`** (_Optional_): [Text](../../guide/types/#text)  
The username of the user you want to return. Only limited information will be returned based on your permissions when making the request.

#### Return value: [Dictionary](../../guide/types/#dictionary)

Returns a dictionary described by the properties below.

- **`id`**: [Text](../../guide/types/#text)  
The user id of the returned user.
- **`username`**: [Text](../../guide/types/#text)  
The username of the returned user.
- **`fullName`**: [Text](../../guide/types/#text)  
The user's first and last name.
- **`email`**: [Text](../../guide/types/#text)  
The email address associated with the user's account.
- **`groups`**: [Text[]](../../guide/types/#text)  
An array of groups that the user belongs to.
- **`role`**: [Text](../../guide/types/#text)  
The role that the user plays within their organization (e.g. Administrator, Publisher, User, Viewer, or Custom).
- **`privileges`**: [Text[]](../../guide/types/#text)  
An array of privileges that the user has within their organization (e.g. edit, view, etc).

#### Example

Returns information about the user "tester".

```arcade
GetUser($layer, "tester")
// returns {"id": "12", "username": "tester", "name":"Testy Tester", "email": "tester@example.com", ...}
```


<a name="getuser3"></a>
### GetUser( portalObject, extensions? ) -> [Dictionary](../../guide/types/#dictionary)

**[Since version 1.12](../../guide/version-matrix)**

**Profiles**: [Attribute Rules](../../guide/profiles/#attribute-rules) | [Popups](../../guide/profiles/#popups) | [Field Calculation](../../guide/profiles/#field-calculation) | [Tasks](../../guide/profiles/#tasks)

Returns the current user from the workspace. For data from a service, either the Portal user or Server user is returned. For data from a database connection, the database user is returned. When no user is associated with the workspace, such as a file geodatabase, an empty string will be returned.

#### Parameters

- **`portalObject`**: [Portal](../../guide/types/#portal)  
A Portal from which to return the current user.
- **`extensions`** (_Optional_): [Boolean](../../guide/types/#boolean)  
Determines if the `userLicenseTypeExtensions` will be returned in the dictionary.

#### Return value: [Dictionary](../../guide/types/#dictionary)

Returns a dictionary described by the properties below.

- **`id`**: [Text](../../guide/types/#text)  
The user id of the returned user.
- **`username`**: [Text](../../guide/types/#text)  
The username of the returned user.
- **`fullName`**: [Text](../../guide/types/#text)  
The user's first and last name.
- **`email`**: [Text](../../guide/types/#text)  
The email address associated with the user's account.
- **`groups`**: [Text[]](../../guide/types/#text)  
An array of groups that the user belongs to.
- **`role`**: [Text](../../guide/types/#text)  
The role that the user plays within their organization (e.g. Administrator, Publisher, User, Viewer, or Custom).
- **`privileges`**: [Text[]](../../guide/types/#text)  
An array of privileges that the user has within their organization (e.g. edit, view, etc).
- **`userLicenseTypeExtensions`**: [Text[]](../../guide/types/#text)  
An array of the license type extensions associated with the user's account (e.g. "Utility Network", "Parcel Fabric", etc). The `extensions` parameter must be set to `true` in order for this to be returned.

#### Example

Returns information about the user currently logged in based on the portal with user extensions.

```arcade
GetUser(Portal('https://www.arcgis.com', true)
```


<a name="getuser4"></a>
### GetUser( features, extensions? ) -> [Dictionary](../../guide/types/#dictionary)

**[Since version 1.12](../../guide/version-matrix)**

**Profiles**: [Attribute Rules](../../guide/profiles/#attribute-rules) | [Popups](../../guide/profiles/#popups) | [Field Calculation](../../guide/profiles/#field-calculation) | [Tasks](../../guide/profiles/#tasks)

Returns the current user from the workspace. For data from a service, either the Portal user or Server user is returned. For data from a database connection, the database user is returned. When no user is associated with the workspace, such as a file geodatabase, an empty string will be returned.

#### Parameters

- **`features`**: [Portal](../../guide/types/#portal)  
A FeatureSet or Portal from which to return the current user.
- **`extensions`** (_Optional_): [Boolean](../../guide/types/#boolean)  
Determines if the `userLicenseTypeExtensions` will be returned in the dictionary.

#### Return value: [Dictionary](../../guide/types/#dictionary)

Returns a dictionary described by the properties below.

- **`id`**: [Text](../../guide/types/#text)  
The user id of the returned user.
- **`username`**: [Text](../../guide/types/#text)  
The username of the returned user.
- **`fullName`**: [Text](../../guide/types/#text)  
The user's first and last name.
- **`email`**: [Text](../../guide/types/#text)  
The email address associated with the user's account.
- **`groups`**: [Text[]](../../guide/types/#text)  
An array of groups that the user belongs to.
- **`role`**: [Text](../../guide/types/#text)  
The role that the user plays within their organization (e.g. Administrator, Publisher, User, Viewer, or Custom).
- **`privileges`**: [Text[]](../../guide/types/#text)  
An array of privileges that the user has within their organization (e.g. edit, view, etc).
- **`userLicenseTypeExtensions`**: [Text[]](../../guide/types/#text)  
An array of the license type extensions associated with the user's account (e.g. "Utility Network", "Parcel Fabric", etc). The `extensions` parameter must be set to `true` in order for this to be returned.

#### Example

Returns information about the user currently logged in based on the workspace connection from a layer with user extensions.

```arcade
GetUser($layer, true)
```


---------------------

## GroupBy

### GroupBy( features, groupByFields, statistics ) -> [FeatureSet](../../guide/types/#featureset)

**[Since version 1.8](../../guide/version-matrix)**

**Profiles**: [Attribute Rules](../../guide/profiles/#attribute-rules) | [Dashboard Data](../../guide/profiles/#dashboard-data) | [Field Calculation](../../guide/profiles/#field-calculation) | [Popups](../../guide/profiles/#popups) | [Tasks](../../guide/profiles/#tasks)

Returns statistics as a FeatureSet for a set of grouped or distinct values.

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
A FeatureSet from which to return statistics for unique values returned from a given set of fields and/or expressions.
- **`groupByFields`**: [Text](../../guide/types/#text) \| [Text[]](../../guide/types/#text) \| [Dictionary[]](../../guide/types/#dictionary)  
The field(s) and/or expression(s) from which to group statistics by unique values. This parameter can be a single field name, an array of field names, or an array of objects that specify column names paired with an expression (typically the field name) for the output FeatureSet. If an array of objects is specified, the following specification must be followed for each object.

 | Property | Description | | :--- | :--- | | name | The name of the column to store the result of the given expression. | | expression | A SQL-92 expression from which to group statistics. This is typically a field name. |
- **`statistics`**: [Dictionary](../../guide/types/#dictionary) \| [Dictionary[]](../../guide/types/#dictionary)  
The summary statistics to calculate for each group. This parameter can be an object or array of objects that specify output statistics to return for each group. The specification in the following table must be used.

 | Property | Description | | :------- | :---------- | | name | The name of the column to store the result of the given statistical query in the output FeatureSet. | | expression | A SQL-92 expression or field name from which to query statistics. | | statistic | The statistic type to query for the given field or expression. **Possible Values:**  SUM \| COUNT \| MIN \| MAX \| AVG \| STDEV \| VAR |

#### Return value: [FeatureSet](../../guide/types/#featureset)

#### Example

Returns the count of each tree type

```arcade
var treeStats = GroupBy($layer, 'TreeType', { name: 'NumTrees', expression: '1', statistic: 'COUNT' });
// treeStats contains features with columns TreeType and NumTrees
// Each unique tree type will have a count
```

Returns the count and the average height of each tree type

```arcade
var treeStats = GroupBy($layer,
  [  // fields/expressions to group statistics by
    { name: 'Type', expression: 'TreeType'},
    { name: 'Status', expression: 'TreeStatus'}
  ], 
  [  // statistics to return for each unique category
    { name: 'Total', expression: '1', statistic: 'COUNT' }, 
    { name: 'AvgHeight', expression: 'Height', statistic: 'AVG' }, 
    { name: 'MaxPercentCoverage', expression: 'CoverageRatio * 100', statistic: 'MAX' }
  ]
);
// treeStats contains features with columns Type, Status, Total, AvgHeight, MaxPercentCoverage
// Each unique tree type (combination of type and status) will have a count, average height, and maximum value of percent coverage
```


---------------------

## Guid

### Guid( guidFormat? ) -> [Text](../../guide/types/#text)

**[Since version 1.3](../../guide/version-matrix)**

Returns a random GUID as a string.

#### Parameters

- **`guidFormat`** (_Optional_): [Text](../../guide/types/#text)  
An named format for the GUID. The default value is `digits-hyphen-braces`.

 **Possible Values:** digits / digits-hyphen / digits-hyphen-braces / digits-hyphen-parentheses

#### Return value: [Text](../../guide/types/#text)

#### Example

Returns a value similar to `{db894515-ed21-4df1-af67-36232256f59a}`

```arcade
Guid()
```

Returns a value similar to `d00cf4dffb184caeb8ed105b2228c247`

```arcade
Guid('digits')
```


---------------------

## Hash

### Hash( value ) -> [Number](../../guide/types/#number)

**[Since version 1.12](../../guide/version-matrix)**

Generates a hash code value for the given variable.

#### Parameters

- **`value`**: [Text](../../guide/types/#text) \| [Number](../../guide/types/#number) \| [Boolean](../../guide/types/#boolean) \| [Date](../../guide/types/#date) \| [Array](../../guide/types/#array) \| [Dictionary](../../guide/types/#dictionary) \| [Geometry](../../guide/types/#geometry)  
The variable to be hashed.

#### Return value: [Number](../../guide/types/#number)

#### Example

Returns `1649420691`.

```arcade
Hash('text value')
```


---------------------

## HasKey

### HasKey( dictionaryOrFeature, keyOrFieldName ) -> [Boolean](../../guide/types/#boolean)

Indicates whether a dictionary or feature has the input key.

#### Parameters

- **`dictionaryOrFeature`**: [Dictionary](../../guide/types/#dictionary) \| [Feature](../../guide/types/#feature)  
The dictionary or feature to check for a key or field name.
- **`keyOrFieldName`**: [Text](../../guide/types/#text)  
The key or field name to check.

#### Return value: [Boolean](../../guide/types/#boolean)

#### Example

prints `true`

```arcade
var d = Dictionary('Port Hope', 16214,  'Grafton', '<1000', 'Cobourg', 18519);
HasKey(d, 'Cobourg');
```


---------------------

## Includes

### Includes( array, value ) -> [Boolean](../../guide/types/#boolean)

**[Since version 1.12](../../guide/version-matrix)**

Determines whether an array contains a given value. Returns `true` if the value is found within the array.

#### Parameters

- **`array`**: [Array](../../guide/types/#array)  
The input array.
- **`value`**: *  
The value to look for in the given array.

#### Return value: [Boolean](../../guide/types/#boolean)

#### Example

Returns `true`.

```arcade
Includes(['orange', 'purple', 'gray'], 'purple')
```

Returns `false`.

```arcade
Includes(['orange', 'purple', 'gray'], 'red')
```


---------------------

## IndexOf

### IndexOf( array, value ) -> [Number](../../guide/types/#number)

Returns the zero-based index location of the input item in an array. If `item` does not exist, then `-1` is returned.

#### Parameters

- **`array`**: [Array](../../guide/types/#array)  
The array to search.
- **`value`**: *  
The item to locate in the array.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints 2

```arcade
var num = [1,2,3,4];
return indexof(num, 3);
```


---------------------

## Insert

### Insert( array, index, value ) -> Null

**[Since version 1.12](../../guide/version-matrix)**

Inserts a new value into an array at a given index. Existing elements positioned at or above the given index will shift up one index value. The array increases in size by one.

#### Parameters

- **`array`**: [Array](../../guide/types/#array)  
The array to insert the new value into.
- **`index`**: [Number](../../guide/types/#number)  
The index of the array where the new value should be inserted. An index of 0 will insert the value at the beginning of the array. An index that equals the size of the array will insert the value at the end of the array. An index greater than the size of the array will cause an error.  If a negative index is provided, it will be used as an offset from the end of the array.
- **`value`**: *  
The value to insert into the array.

#### Example

```arcade
var colors = ['orange', 'purple', 'gray']
Insert(colors, 1, 'yellow')
// colors = ['orange','yellow','purple','gray']
```

```arcade
var colors = ['orange', 'purple', 'gray']
Insert(colors, -1, 'yellow')
// colors = ['orange','purple','yellow','gray']
```


---------------------

## IsEmpty

### IsEmpty( value ) -> [Boolean](../../guide/types/#boolean)

Returns `true` if the provided value is `null` or an empty string (e.g. `''`). Returns `false` for all other cases, including empty arrays and dictionaries.

#### Parameters

- **`value`**: *  
The value that is compared against `null` or `''`. This may be a value of any type.

#### Return value: [Boolean](../../guide/types/#boolean)

#### Example

```arcade
// Returns true
IsEmpty(null)
```

```arcade
// Returns false
IsEmpty('hello world')
```


---------------------

## IsNan

### IsNan( value ) -> [Boolean](../../guide/types/#boolean)

**[Since version 1.5](../../guide/version-matrix)**

Indicates whether the input value is not a number (NaN). A number is considered NaN in one of the following scenarios: - `0/0` - `Infinity / Infinity` - `Infinity * 0` - Any operation in which NaN is an operand - Casting a non-numeric string or `undefined` to a number

#### Parameters

- **`value`**: *  
The value to check if it is NaN.

#### Return value: [Boolean](../../guide/types/#boolean)

#### Example

```arcade
// Returns true
IsNan(Infinity / Infinity)
```

```arcade
// Returns false
IsNan('4')
```


---------------------

## Map

### Map( array, mappingFunction ) -> [Array](../../guide/types/#array)

**[Since version 1.16](../../guide/version-matrix)**

Creates a new array based on results of calling a provided function on each element in the input array.

#### Parameters

- **`array`**: [Array](../../guide/types/#array)  
The input array to map.
- **`mappingFunction`**: [Function](../../guide/logic/#user-defined-functions)  
The function to call on each element in the provided array. This must be a user-defined function or a core Arcade function defined with the following parameters:

 **Parameters**  
 `value`: Represents the value of an element in the array.

 **Return value**  
 The function may return any value in the output array.

#### Return value: [Array](../../guide/types/#array)

#### Example

Converts all of the elements in the array from Fahrenheit to Celsius and returns them in a new array.

```arcade
// This function will take in values from the input array and convert them to Celsius
function toCelsius(f) {
  return Round((f - 32) * 5/9, 2) } 
}
// The toCelsius function executes for each each item
// in the input array.
// Map returns the resulting array of converted values.
Map([82, 67, 96, 55, 34], toCelsius)
// returns [27.78, 19.44, 35.56, 12.78, 1.11]
```

Converts date objects to formatted text

```arcade
var dates = [ Date(1996, 11, 10), Date(1995, 1, 6), Date(1992, 2, 27), Date(1990, 10, 2)];
function formatDates(dateVal) { return Text(dateVal, 'MMM D, Y') }
Map(dates, formatDates);
// returns ['Dec 10, 1996', 'Feb 6, 1995', 'Mar 27, 1992', 'Nov 2, 1990']
```


---------------------

## NextSequenceValue

### NextSequenceValue( sequenceName ) -> [Number](../../guide/types/#number)

**[Since version 1.4](../../guide/version-matrix)**

**Profiles**: [Attribute Rule Calculation](../../guide/profiles/#attribute-rule-calculation)

Returns the next sequence value from the database sequence specified. If `inputSequenceName` does not exist, the expression will error.

#### Parameters

- **`sequenceName`**: [Text](../../guide/types/#text)  
The name of the sequence. This must already be configured in the database.

#### Return value: [Number](../../guide/types/#number)

#### Example

Returns a number with the next sequence value

```arcade
NextSequenceValue('PipeIDSeq')
```


---------------------

## None

### None( array, testFunction ) -> [Boolean](../../guide/types/#boolean)

**[Since version 1.16](../../guide/version-matrix)**

Tests whether none of the elements in a given array pass a test from the provided function. Returns `true` if the `testFunction` returns `false` for all items in the input array.

#### Parameters

- **`array`**: [Array](../../guide/types/#array)  
The input array to test.
- **`testFunction`**: [Function](../../guide/logic/#user-defined-functions)  
The function to test each element in the `inputArray`. This must be a user-defined function or a core Arcade function defined with the following parameters:

 **Parameters**  : `value`: Represents the value of an element in the array.

 **Return value**  
 The function must return either `true` or `false` indicating whether the element passed or failed the test.

#### Return value: [Boolean](../../guide/types/#boolean)

#### Example

Returns `false` because some of the elements in the input array pass the `isEven` test

```arcade
// isEven is used to test if each element in the array is even
// it returns true if the element is divisible by two, false if is not
function isEven(value) { return value % 2 == 0 } 
// The isEven function will execute for each element in the array,
// returning the following values: false, true, false, true, false
// Since at least one value in the array passed the test
// (return true), the return value will be false
None([1,2,3,4,5], isEven)
```

Uses the existing `isEmpty` Arcade function as the `testFunction`. This is valid because `isEmpty` takes a single parameter and returns a boolean value. This expression returns `true` if none of the fields are empty.

```arcade
var myArray = [ $feature.field1, $feature.field2, $feature.field3, $feature.field4];
None(myArray, isEmpty)
```


---------------------

## Number

### Number( value, pattern? ) -> [Number](../../guide/types/#number)

Parses the input value to a number.

#### Parameters

- **`value`**: *  
The value to convert to a number.
- **`pattern`** (_Optional_): [Text](../../guide/types/#text)  
The format pattern string used to parse numbers formatted in a localized context from a string value to a number. The table below describes the characters that may be used in the pattern.

 | **Value** | **Description** | | :--- | :--- | | 0 | Mandatory digits | | # | Optional digits | | % | Divide by 100 |

#### Return value: [Number](../../guide/types/#number)

#### Example

###### Parses a number using a grouping separator appropriate for the local in which the expression is executed
returns 1365

```arcade
Number('1,365', ',###')
```

###### Remove strings from number.
prints 10

```arcade
Number('abc10def', 'abc##def')
```

###### Specify minimum digits past 0 as two and maximum digits past 0 as 4.
prints 10.456

```arcade
Number('10.456','00.00##')
```

###### Specify minimum digits past 0 as two and maximum digits past 0 as 4. The left and right side of the function must match or NaN is returned.
prints NaN

```arcade
Number('10.4','00.00##')
```

###### Indicate the size of the repeated group and the final group size of the input value.
prints 1212456

```arcade
Number('12,12,456', ',##,###')
```

###### If there is a negative subpattern, it serves only to specify the negative prefix and suffix.
prints -1223345

```arcade
Number('-12,23,345', ',##,###;-,##,###')
```

###### Divide by 100. Maximum of three decimal places can be input.
prints 0.9999

```arcade
Number('99.99%', '#.##%')
```


---------------------

## OrderBy

### OrderBy( features, sqlExpression ) -> [FeatureSet](../../guide/types/#featureset)

**[Since version 1.5](../../guide/version-matrix)**

**Profiles**: [Attribute Rules](../../guide/profiles/#attribute-rules) | [Dashboard Data](../../guide/profiles/#dashboard-data) | [Popups](../../guide/profiles/#popups) | [Field Calculation](../../guide/profiles/#field-calculation) | [Tasks](../../guide/profiles/#tasks)

Orders a FeatureSet by using a SQL92 OrderBy clause.

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
The FeatureSet, or layer, to order.
- **`sqlExpression`**: [Text](../../guide/types/#text)  
The SQL92 expression used to order features in the layer.

#### Return value: [FeatureSet](../../guide/types/#featureset)

#### Example

###### Order features by population where features with the highest population are listed first
```arcade
OrderBy($layer, 'POPULATION DESC')
```

###### Order features by rank in ascending order
```arcade
OrderBy($layer, 'Rank ASC')
```


---------------------

## Pop

### Pop( array ) -> *

**[Since version 1.12](../../guide/version-matrix)**

Removes and returns the element at the end of the array. If the array is empty, then an error is thrown.

#### Parameters

- **`array`**: [Array](../../guide/types/#array)  
The input array from which the last element will be removed and returned.

#### Return value: *

#### Example

Returns 'gray'. The input array will now equal `['orange', 'purple']`.

```arcade
Pop(['orange', 'purple', 'gray'])
```


---------------------

## Portal

### Portal( url ) -> [Portal](../../guide/types/#portal)

**[Since version 1.8](../../guide/version-matrix)**

**Profiles**: [Field Calculation](../../guide/profiles/#field-calculation) | [Popups](../../guide/profiles/#popups) | [Tasks](../../guide/profiles/#tasks)

Creates a reference to an ArcGIS Portal.

#### Parameters

- **`url`**: [Text](../../guide/types/#text)  
The url of the portal.

#### Return value: [Portal](../../guide/types/#portal)

#### Example

Query features from a portal item in ArcGIS Online

```arcade
var arcgisPortal = Portal('https://www.arcgis.com');
var features = FeatureSetByPortalItem(arcgisPortal, '7b1fb95ab77f40bf8aa09c8b59045449', 0, ['Name', 'Count'], false);
```

Enterprise Portal

```arcade
Portal('https://www.example.com/arcgis')
```


---------------------

## Push

### Push( array, value ) -> [Number](../../guide/types/#number)

**[Since version 1.12](../../guide/version-matrix)**

Adds an element to the end of an array and returns the new length of the array.

#### Parameters

- **`array`**: [Array](../../guide/types/#array)  
The array to have elements pushed to.
- **`value`**: *  
The value to add as the last element of the input array.

#### Return value: [Number](../../guide/types/#number)

#### Example

Returns 4. The input array will now equal `['orange', 'purple', 'gray', 'red']`.

```arcade
Push(['orange', 'purple', 'gray'], 'red').
```


---------------------

## Reduce

### Reduce( array, reducerFunction, initialValue? ) -> *

**[Since version 1.16](../../guide/version-matrix)**

Executes a provided "reducer" function on each element in the array, passing in the return value from the calculation of the previous element.

#### Parameters

- **`array`**: [Array](../../guide/types/#array)  
The input array to reduce.
- **`reducerFunction`**: [Function](../../guide/logic/#user-defined-functions)  
The reducer function.

 **Parameters**  
 **`previousValue`:** The previous value returned from the `reducerFunction`. The first time the function executes, this will be the first element in the `inputArray` (or the `initialValue`, if provided).  
 **`arrayValue`:** Represents the current value of an element in the `inputArray`.

 **Return value**  
 Returns a value that will be passed back into the function as the `previousValue` parameter.
- **`initialValue`** (_Optional_): *  
An item to pass into the first argument of the reducer function.

#### Return value: *

#### Example

Without the `initialValue` parameter, the first two elements of the `cities` array are passed into the add function as arguments.

```arcade
var cities = [{
   name: 'Columbus',
   pop: 913921
}, {
   name: 'Cincinnati',
   pop: 307266
}, {
   name: 'Dayton',
   pop: 140343
}, {
   name: 'Cleveland',
   pop: 376599
}];
// the first time this function is called it will take the first two elements of the array as x and y
// The subsequent times the function is executed, it will take the return value
// from the previous function call as x and the next array value as y
function mostPopulated(city1, city2) {
   iif (city1.pop > city2.pop, city1, city2)
}
var largestCity = Reduce(cities, mostPopulated)
Console(largestCity.name + ' is the biggest city in the list with a population of ' + largestCity.pop)
// Columbus is the biggest city in the list with a population of 913921
```

Since the `initialValue` parameter is set, that value will be the function's first argument (`city1`), and the first element of the `cities` will be the function's second argument (`city2`).

```arcade
var los_angeles = { name: 'Los Angeles', pop: 3898747 }
// since an initialValue is provided, it will be passed into the maxPop function as x
// and the first value of the array will be passed in as y for the initial function call
// The subsequent times the function is executed, it will take the return value
// from the previous function call as x and the next array value as y
var largestCity = Reduce(cities, mostPopulated, los_angeles)
Console(largestCity.name + ' is the biggest city in the list with a population of ' + largestCity.pop)
// Los Angeles is the biggest city in the list with a population of 3898747
```


---------------------

## Resize

### Resize( array, newSize, value? ) -> Null

**[Since version 1.12](../../guide/version-matrix)**

Changes the number of elements in an array to the specified size. It can be used to expand the array or truncate it early. After resizing, attempting to index beyond the new last element will result in an error, except for the case of indexing the next element, which will continue to expand the array by one element.

#### Parameters

- **`array`**: [Array](../../guide/types/#array)  
The array to be resized.
- **`newSize`**: [Number](../../guide/types/#number)  
The number of elements desired in the resized array.
- **`value`** (_Optional_): *  
The optional value that will be used for any new elements added to the array. If no value is specified, the newly added elements will have a `null` value.

#### Example

Returns `['orange', 'purple', 'gray', null, null]`

```arcade
var colors = ['orange', 'purple', 'gray']
Resize(colors, 5)
return colors
```

Returns `['orange', 'purple', 'gray', 'red', 'red']`

```arcade
var colors = ['orange', 'purple', 'gray']
Resize(colors, 5, 'red')
return colors
```

Returns `['orange']`

```arcade
var colors = ['orange', 'purple', 'gray']
Resize(colors, 1)
return colors
```


---------------------

## Reverse

### Reverse( array ) -> [Array](../../guide/types/#array)

Reverses the contents of the array in place.

#### Parameters

- **`array`**: [Array](../../guide/types/#array)  
The array to be reversed.

#### Return value: [Array](../../guide/types/#array)

#### Example

Returns `['gray', 'purple', 'orange']`

```arcade
Reverse(['orange', 'purple', 'gray'])
```


---------------------

## Schema

This function has 2 signatures:

- [Schema( feature ) -> Dictionary](#schema1)
- [Schema( features ) -> Dictionary](#schema2)

<a name="schema1"></a>
### Schema( feature ) -> [Dictionary](../../guide/types/#dictionary)

**[Since version 1.11](../../guide/version-matrix)**

**Profiles**: [Attribute Rules](../../guide/profiles/#attribute-rules) | [Dashboard Data](../../guide/profiles/#dashboard-data) | [Popups](../../guide/profiles/#popups) | [Field Calculation](../../guide/profiles/#field-calculation) | [Velocity](../../guide/profiles/#velocity) | [Tasks](../../guide/profiles/#tasks)

Returns the schema description of the provided Feature.

#### Parameters

- **`feature`**: [Feature](../../guide/types/#feature)  
The feature whose schema to return.

#### Return value: [Dictionary](../../guide/types/#dictionary)

Returns a dictionary described by the properties below.

- **`fields`**: [Dictionary[]](../../guide/types/#dictionary)  
Returns an array of dictionaries describing the fields in the Feature. Each dictionary describes the field `name`, `alias`, `type`, `subtype`, `domain`, `length`, and whether it is `editable` and `nullable`.
- **`geometryType`**: [Text](../../guide/types/#text)  
The geometry type of features in the Feature. Returns `esriGeometryNull` for tables with no geometry.

 **Possible values:** `esriGeometryPoint`, `esriGeometryLine`, `esriGeometryPolygon`, `esriGeometryNull`
- **`globalIdField`**: [Text](../../guide/types/#text)  
The global ID field of the Feature. Returns `""` if not globalId-enabled.
- **`objectIdField`**: [Text](../../guide/types/#text)  
The objectId field of the Feature.
<a name="schema2"></a>
### Schema( features ) -> [Dictionary](../../guide/types/#dictionary)

**[Since version 1.11](../../guide/version-matrix)**

**Profiles**: [Attribute Rules](../../guide/profiles/#attribute-rules) | [Dashboard Data](../../guide/profiles/#dashboard-data) | [Popups](../../guide/profiles/#popups) | [Field Calculation](../../guide/profiles/#field-calculation) | [Velocity](../../guide/profiles/#velocity) | [Tasks](../../guide/profiles/#tasks)

Returns the schema description of the provided FeatureSet.

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
The FeatureSet whose schema to return.

#### Return value: [Dictionary](../../guide/types/#dictionary)

Returns a dictionary described by the properties below.

- **`objectIdField`**: [Text](../../guide/types/#text)  
The objectId field of the FeatureSet.
- **`globalIdField`**: [Text](../../guide/types/#text)  
The global ID field of the FeatureSet. Returns `""` if not globalId-enabled.
- **`geometryType`**: [Text](../../guide/types/#text)  
The geometry type of features in the FeatureSet. Returns `esriGeometryNull` for tables with no geometry.

 **Possible values:** `esriGeometryPoint`, `esriGeometryLine`, `esriGeometryPolygon`, `esriGeometryNull`
- **`fields`**: [Dictionary[]](../../guide/types/#dictionary)  
Returns an array of dictionaries describing the fields in the FeatureSet. Each dictionary describes the field `name`, `alias`, `type`, `subtype`, `domain`, `length`, and whether it is `editable` and `nullable`.
---------------------

## Slice

### Slice( array, startIndex?, endIndex? ) -> [Array](../../guide/types/#array)

**[Since version 1.12](../../guide/version-matrix)**

Returns a copy of the contents of a portion of an array between two indexes as a new array.

#### Parameters

- **`array`**: [Array](../../guide/types/#array)  
The array to be sliced.
- **`startIndex`** (_Optional_): [Number](../../guide/types/#number)  
The index from which to start the slice. Defaults to `0`. If a negative index is provided, it will be used as an offset from the end of the array.
- **`endIndex`** (_Optional_): [Number](../../guide/types/#number)  
The index where the slice will end. The value at this index will not be included in the returned array. Defaults to the array size.

#### Return value: [Array](../../guide/types/#array)

#### Example

Returns `['purple', 'gray']`

```arcade
Slice(['orange', 'purple', 'gray', 'red', 'blue'], 1, 3)
```

Returns `['red', 'blue']`

```arcade
Slice(['orange', 'purple', 'gray', 'red', 'blue'], 3)
```

Returns `['orange', 'purple', 'gray', 'red', 'blue']`

```arcade
Slice(['orange', 'purple', 'gray', 'red', 'blue'])
```

Returns `['blue']`

```arcade
Slice(['orange', 'purple', 'gray', 'red', 'blue'], -1)
```


---------------------

## Sort

### Sort( array, comparatorFunction? ) -> [Array](../../guide/types/#array)

Sorts an array by ASCII value. If all the items in the array are the same type, an appropriate sort function will be used. If they are different types, the items will be converted to strings. If the array contains objects, and no user defined function is provided, no sort will happen.

#### Parameters

- **`array`**: [Array](../../guide/types/#array)  
The array to sort.
- **`comparatorFunction`** (_Optional_): [Function](../../guide/logic/#user-defined-functions)  
A user defined function to be used for the sort.

 **Parameters**  
 **`a`:** The first element for comparison.  
 **`b`:** The second element for comparison.

 **Return value**  
 **`number`:** A number indicating how `a` and `b` should be sorted. If the number is > 0, sort `b` before `a`. If < 0, sort `a` before `b`. If 0 is returned, keep the original order of `a` and `b`.

#### Return value: [Array](../../guide/types/#array)

#### Example

returns `['$', 1, 'A', 'a']`

```arcade
Sort([1, 'a', '$', 'A'])
```

###### Sort using a user defined function
returns '[{ 'AGE': 24, 'NAME': 'Emma' }, { 'AGE': 25, 'NAME': 'Sam' }, { 'AGE': 27, 'NAME': 'Bob' } ]'

```arcade
var peopleArray = [{ 'NAME': 'Sam', 'AGE': 25 }, {'NAME': 'Bob', 'AGE': 27 },{ 'NAME': 'Emma', 'AGE': 24 }];
function compareAge(a,b){
  if (a['AGE']<b['AGE'])
    return -1;
  if (a['AGE']>b['AGE'])
    return 1;
  return 0;
}
return Sort(peopleArray, compareAge);
```


---------------------

## Splice

### Splice( value1, [value2, ..., valueN]? ) -> [Array](../../guide/types/#array)

**[Since version 1.12](../../guide/version-matrix)**

Concatenates all parameters together into a new array.

#### Parameters

- **`value1`**: *  
A value to be spliced into a new array.
- **`[value2, ..., valueN]`** (_Optional_): *  
Ongoing values to be spliced into a new array.

#### Return value: [Array](../../guide/types/#array)

#### Example

Returns `['orange', 'purple', 1, 2, 'red']`

```arcade
Splice(['orange', 'purple'], 1, 2, 'red')
```

Returns `[1, 2, 3, 4]`

```arcade
Splice([1,2], [3,4])
```


---------------------

## SubtypeCode

### SubtypeCode( feature ) -> [Number](../../guide/types/#number) \| [Text](../../guide/types/#text) \| [Date](../../guide/types/#date)

**[Since version 1.11](../../guide/version-matrix)**

Returns the subtype code for a given feature.

#### Parameters

- **`feature`**: [Feature](../../guide/types/#feature)  
The Feature from which to get the subtype code.

#### Return value: [Number](../../guide/types/#number) \| [Text](../../guide/types/#text) \| [Date](../../guide/types/#date)

#### Example

Returns the code of the subtype

```arcade
// feature has a field named `assetGroup`
// with the subtype described in the Subtypes function example
SubtypeCode($feature)  // returns 1
```


---------------------

## SubtypeName

### SubtypeName( feature ) -> [Text](../../guide/types/#text)

**[Since version 1.11](../../guide/version-matrix)**

Returns the subtype name for a given feature.

#### Parameters

- **`feature`**: [Feature](../../guide/types/#feature)  
The Feature from which to get the subtype name.

#### Return value: [Text](../../guide/types/#text)

#### Example

Returns the name of the subtype

```arcade
// feature has a field named `assetGroup`
// with the subtype described in the Subtypes function example
SubtypeName($feature) // returns "Single Phase"
```


---------------------

## Subtypes

This function has 2 signatures:

- [Subtypes( feature ) -> Dictionary](#subtypes1)
- [Subtypes( features ) -> Dictionary](#subtypes2)

<a name="subtypes1"></a>
### Subtypes( feature ) -> [Dictionary](../../guide/types/#dictionary)

**[Since version 1.11](../../guide/version-matrix)**

Returns the subtype coded value Dictionary. Returns `null` when subtypes are not enabled on the layer.

#### Parameters

- **`feature`**: [Feature](../../guide/types/#feature)  
The Feature from which to get subtypes.

#### Return value: [Dictionary](../../guide/types/#dictionary)

Returns a dictionary described by the properties below.

- **`subtypeField`**: [Text](../../guide/types/#text)  
The field containing a subtype.
- **`subtypes`**: [Dictionary[]](../../guide/types/#dictionary)  
An array of dictionaries describing the subtypes. Each dictionary has a `code` property, which contains the actual field value, and a `name` property containing a user-friendly description of the value (e.g. `{ code: 1, name: "pavement" }`)

#### Example

Returns subtypes with coded values from a feature

```arcade
Subtypes($feature)
// returns the following dictionary
// {
//   subtypeField: 'assetGroup',
//   subtypes: [
//     { name: "Unknown", code: 0 },
//     { name: "Single Phase", code: 1 },
//     { name: "Two Phase", code: 2 }
//   ]
// }
```


<a name="subtypes2"></a>
### Subtypes( features ) -> [Dictionary](../../guide/types/#dictionary)

**[Since version 1.11](../../guide/version-matrix)**

Returns the subtype coded value Dictionary. Returns `null` when subtypes are not enabled on the layer.

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
The FeatureSet from which to get subtypes.

#### Return value: [Dictionary](../../guide/types/#dictionary)

Returns a dictionary described by the properties below.

- **`subtypeField`**: [Text](../../guide/types/#text)  
The field containing a subtype.
- **`subtypes`**: [Dictionary[]](../../guide/types/#dictionary)  
An array of dictionaries describing the subtypes. Each dictionary has a `code` property, which contains the actual field value, and a `name` property containing a user-friendly description of the value (e.g. `{ code: 1, name: "pavement" }`)

#### Example

Returns subtypes with coded values from a FeatureSet

```arcade
var fsTransformer = FeatureSetByName($layer, "Transformer")
Subtypes(fsTransformer)
// returns the following dictionary
// {
//   subtypeField: 'assetGroup',
//   subtypes: [
//     { name: "Unknown", code: 0 },
//     { name: "Single Phase", code: 1 },
//     { name: "Two Phase", code: 2 }
//   ]
// }
```


---------------------

## ToHex

### ToHex( value ) -> [Text](../../guide/types/#text)

**[Since version 1.12](../../guide/version-matrix)**

Converts an integer to a hexidecimal representation.

#### Parameters

- **`value`**: [Number](../../guide/types/#number)  
The value to be converted to a hexidecimal value.

#### Return value: [Text](../../guide/types/#text)

#### Example

###### Returns `"64"`.
```arcade
ToHex(100)
```

###### Returns the hexidecimal representation for the color royal blue, `"#4169E1"`, from its RGB values
```arcade
var r = ToHex(65); // returns "41"
var g = ToHex(105); // returns "69"
var b = ToHex(225); // returns "E1"
Concatenate("#",r,g,b)
// Returns "#4169E1"
```


---------------------

## Top

This function has 2 signatures:

- [Top( array, numItems ) -> Array](#top1)
- [Top( features, numItems ) -> FeatureSet](#top2)

<a name="top1"></a>
### Top( array, numItems ) -> [Array](../../guide/types/#array)

**[Since version 1.3](../../guide/version-matrix)**

Truncates the input array and returns the first given number of elements.

#### Parameters

- **`array`**: [Array](../../guide/types/#array)  
The array to truncate.
- **`numItems`**: [Number](../../guide/types/#number)  
The number of items to return from the beginning of the array.

#### Return value: [Array](../../guide/types/#array)

#### Example

###### returns `[ 43,32,19 ]`
```arcade
Top([ 43,32,19,0,3,55 ], 3)
```


<a name="top2"></a>
### Top( features, numItems ) -> [FeatureSet](../../guide/types/#featureset)

**[Since version 1.3](../../guide/version-matrix)**

Truncates the FeatureSet and returns the first given number of features.

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
The FeatureSet to truncate.
- **`numItems`**: [Number](../../guide/types/#number)  
The number of features to return from the beginning of the FeatureSet.

#### Return value: [FeatureSet](../../guide/types/#featureset)

#### Example

###### Returns the top 5 features with the highest population
```arcade
Top( OrderBy($layer, 'POPULATION DESC'), 5 )
```


---------------------

## TypeOf

### TypeOf( value ) -> [Text](../../guide/types/#text)

Returns the type of the input value. Will return one of the following types: Array, Date, Text, Boolean, Number, Dictionary, Feature, Point, Polygon, Polyline, Multipoint, Extent, Function, Unrecognized Type.

#### Parameters

- **`value`**: *  
The input value, variable, or feature attribute.

#### Return value: [Text](../../guide/types/#text)

#### Example

prints 'Boolean'

```arcade
TypeOf(true)
```

prints 'Date'

```arcade
TypeOf(Now())
```


---------------------
