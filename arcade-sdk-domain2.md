## Domain( feature, fieldName ) -> `Dictionary`

**[Since version 1.11](../../guide/version-matrix/)**

Returns the domain assigned to the given field of the provided `feature`. If the `feature` belongs to a class with a subtype, this returns the domain assigned to the subtype.

### Parameters
&emsp;**`feature`**: [Feature](../../guide/types/#feature)  
&emsp;The Feature with a field that has a domain.

&emsp;**`fieldName`**: [Text](../../guide/types/#text)  
&emsp;The name of the field (not the alias of the field) assigned the domain.

### Return value: [Dictionary](../../guide/types/#dictionary)

Returns a dictionary described by the properties below:

&emsp;**`type`**: [Text](../../guide/types/#text)  
&emsp;The type of domain - either `codedValue` or `range`.

&emsp;`name`**: [Text](../../guide/types/#text)  
&emsp;The domain name.

&emsp;**`dataType`**: [Text](../../guide/types/#text)  
&emsp;The data type of the domain field. It can be one of the following values: `esriFieldTypeSmallInteger`, `esriFieldTypeInteger`, `esriFieldTypeSingle`, `esriFieldTypeDouble`, `esriFieldTypeString`, `esriFieldTypeDate`, `esriFieldTypeOID`, `esriFieldTypeGeometry`, `esriFieldTypeBlob`, `esriFieldTypeRaster`, `esriFieldTypeGUID`, `esriFieldTypeGlobalID`, `esriFieldTypeXML`.

&emsp;**`min`**: [Number](../../guide/types/#number)  
&emsp;Only applicable to `range` domains. The minimum value of the domain.

&emsp;**`max`**: [Number](../../guide/types/#number)  
&emsp;Only applicable to `range` domains. The maximum value of the domain.

&emsp;**`codedValues`**: [Dictionary[]](../../guide/types/#dictionary)  
&emsp;Only applicable to `codedValue` domains. An array of dictionaries describing the valid values for the field. Each dictionary has a `code` property, which contains the actual field value, and a `name` property containing a user-friendly description of the value (e.g. `{ code: 1, name: "pavement" }`).

### Example

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
