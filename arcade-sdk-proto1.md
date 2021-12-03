### Distinct( features, fields ) -> `FeatureSet`

**[Since version 1.8](../../guide/version-matrix)**

**Profiles**: [Attribute Rules](../../guide/profiles/#attribute-rules) | [Dashboard Data](../../guide/profiles/#dashboard-data) | [Field Calculation](../../guide/profiles/#field-calculation) | [Popups](../../guide/profiles/#popups) | [Tasks](../../guide/profiles/#tasks)

#### Parameters

**`features`**: [FeatureSet](../../guide/types/#featureset)

Returns a set of distinct, or unique, values from a FeatureSet.

**`fields`**: [Text](../../guide/types/#text) \| [Array](../../guide/types/#array) \| [Object](../../guide/types/#object)

The field(s) and/or expression(s) from which to determine unique values. This parameter can be an array of field names, an array of expressions, or an object or array of objects that specify output column names where unique values will be stored. If an object is specified, the following specification must be used:

&nbsp;&nbsp;**`name`**  
&nbsp;&nbsp;The name of the column to store the result of the given expression.

&nbsp;&nbsp;**`expression`**  
&nbsp;&nbsp;A SQL-92 expression from which to calculate a unique value.

#### Return value

[FeatureSet](../../guide/types/#featureset)

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
Distinct(
  $layer,
  {
    name: "Density",
    expression: "CASE WHEN PopDensity < 100 THEN 'Low' WHEN PopDensity >= 100 THEN 'High' ELSE 'N/A' END"
  }
)
```

Returns FeatureSet with a Score and a Type column

```arcade
Distinct($layer, [
  { name: 'Score', expression: 'POPULATION_DENSITY * 0.65 + Status_Code * 0.35' }
  { name: 'Type', expression: 'Category' }
])
```
