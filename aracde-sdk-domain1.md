### Domain( feature, fieldName ) -> `Dictionary`

**[Since version 1.11](../../guide/version-matrix/)**

Returns the domain assigned to the given field of the provided `feature`. If the `feature` belongs to a class with a subtype, this returns the domain assigned to the subtype.

#### Parameters

- **`feature`**: [Feature](../../guide/types/#feature)  
The Feature with a field that has a domain.

- **`fieldName`**: [Text](../../guide/types/#text)  
The name of the field (not the alias of the field) assigned the domain.

#### Returns value: [Dictionary](../../guide/types/#dictionary)

Returns a dictionary described by the properties below:

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
