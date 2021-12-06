---
title: Logical Functions
description: Documentation for all Logical Functions supported in Arcade.
keywords:
  - Decode
  - DefaultValue
  - IIf
  - When
---

# Logical Functions

These functions provide convenient one-line methods for evaluating expressions. They include methods for checking for [empty](#isempty) values, using [if-else](#iif) logic, and implementing [switch-case](#decode) statements among others.

---------------------

## Decode

### Decode( expression, [compare1, return1, ..., compareN, returnN]?, default? ) -> *

Evaluates an expression to a value and compares the result value with the value of subsequent parameters. If the expression evaluates to a matching value, it returns the subsequent parameter value. If no matches are found, then a `default` value may be provided. This is similar to a switch/case statement

#### Parameters

- **`expression`**: *  
An Arcade expression that must evaluate to a value that can be compared with the provided case values.
- **`[compare1, return1, ..., compareN, returnN]`** (_Optional_): *  
A set of compare values and return value pairs.
- **`default`** (_Optional_): *  
A default value to return if none of the compare values match. This may be a value of any type.

#### Return value: *

Returns the matched return value. If no matches are found, then the `default` value is returned.

#### Example

```arcade
// returns a meaningful value when a field contains coded values
var code = $feature.codedValue;
var decodedValue = Decode(code, 1, 'Residential', 2, 'Commercial', 3, 'Mixed', 'Other');
```


---------------------

## DefaultValue

### DefaultValue( value, defaultValue? ) -> *

Returns a specified default value if an empty value is detected.

#### Parameters

- **`value`**: *  
The input value to compare against `null` or `''`. This may be a value of any type. However, if this value is an empty array, then the empty array will be returned.
- **`defaultValue`** (_Optional_): *  
Return this value if the provided `value` is empty. The data type of `defaultValue` must match the data type of `value`.

#### Return value: *

If `value` is empty, then the `defaultValue` is returned. Otherwise, the value of `value` is returned.

#### Example

```arcade
// If a feature has no value in the POP_2000 field
// then 'no data' is returned
DefaultValue($feature.POP_2000, 'no data')
```


---------------------

## IIf

### IIf( condition, trueValue, falseValue ) -> *

Returns a given value if a conditional expression evaluates to `true`, and returns an alternate value if that condition evaluates to `false`.

#### Parameters

- **`condition`**: [Boolean](../../guide/types/#boolean)  
A logical expression that must evaluate to `true` or `false`.
- **`trueValue`**: *  
The value to return if the `condition` evaluates to `true`. This may be a value of any type.
- **`falseValue`**: *  
The value to return if the `condition` evaluates to `false`. This may be a value of any type.

#### Return value: *

If `condition` is `true`, then the `trueValue` is returned. Otherwise, the value of `falseValue` is returned.

#### Example

```arcade
// returns 'below' if the value is less than 1,000,000.
// if the value is more than 1,000,000, then returns 'above'
var population = $feature.POP_2007;
IIf(population < 1000000, 'below', 'above');
```


---------------------

## When

### When( [expression1, result1, ..., expressionN, resultN], defaultValue ) -> *

Evaluates a series of conditional expressions until one evaluates to `true`.

#### Parameters

- **`[expression1, result1, ..., expressionN, resultN]`**: *  
A series of conditional expressions and return values if the given expression evaluates to `true`. This may be a value of any type.
- **`defaultValue`**: *  
Returns this value if all expressions evaluate to `false`. This may be a value of any type.

#### Return value: *

#### Example

Reclassify a numeric field value to a generic ranking (string).  
If all expressions are `false`, then 'n/a' is returned

```arcade
var density = $feature.densityField;
var ranking = When(density < 50, 'low', density >=50 && density < 100, 'medium', density >= 100, 'high', 'n/a');
```


---------------------