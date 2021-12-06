---
title: Mathematical Functions
description: Documentation for all Mathematical Functions supported in Arcade.
keywords:
  - Abs
  - Acos
  - Asin
  - Atan
  - Atan2
  - Average
  - Ceil
  - Constrain
  - Cos
  - Exp
  - Floor
  - Log
  - Max
  - Mean
  - Min
  - Pow
  - Random
  - Round
  - Sin
  - Sqrt
  - Stdev
  - Sum
  - Tan
  - Variance
---

# Mathematical Functions

Functions for performing mathematical operations.

---------------------

## Abs

### Abs( value ) -> [Number](../../guide/types/#number)

Returns the absolute value of a number. If the input is `null`, then it returns 0.

#### Parameters

- **`value`**: [Number](../../guide/types/#number)  
A number on which to perform the operation.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints 3

```arcade
Abs(-3)
```


---------------------

## Acos

### Acos( value ) -> [Number](../../guide/types/#number)

Returns the arccosine of the input value in radians, in the range of zero to PI. If the input value is outside the appropriate range of +/- 1, then NaN is returned.

#### Parameters

- **`value`**: [Number](../../guide/types/#number)  
A number between -1 and 1 on which to perform the operation.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints 1.266104

```arcade
Acos(0.3)
```


---------------------

## Asin

### Asin( value ) -> [Number](../../guide/types/#number)

Returns the arcsine of the input value in radians, in the range of -PI/2 and PI/2. If the input value is outside the appropriate range of +/- 1, then NaN is returned.

#### Parameters

- **`value`**: [Number](../../guide/types/#number)  
A number between -1 and 1 on which to perform the operation.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints 0.304693

```arcade
Asin(0.3)
```


---------------------

## Atan

### Atan( value ) -> [Number](../../guide/types/#number)

Returns the arctangent of the input value in radians, in the range of -PI/2 and PI/2.

#### Parameters

- **`value`**: [Number](../../guide/types/#number)  
A number on which to perform the operation.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints 0.785398

```arcade
Atan(1)
```


---------------------

## Atan2

### Atan2( y, x ) -> [Number](../../guide/types/#number)

Returns the arctangent of the quotient of the input values in radians, in the range of -PI and zero or zero and PI depending on the sign of arguments.

#### Parameters

- **`y`**: [Number](../../guide/types/#number)  
A number representing the y-coordinate.
- **`x`**: [Number](../../guide/types/#number)  
A number representing the x-coordinate.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints -2.356194

```arcade
Atan2(-1, -1)
```


---------------------

## Average

This function has 2 signatures:

- [Average( numbers ) -> Number](#average1)
- [Average( features, fieldNameOrSQLExpression ) -> Number](#average2)

<a name="average1"></a>
### Average( numbers ) -> [Number](../../guide/types/#number)

Returns the average of a set of numbers.

#### Parameters

- **`numbers`**: [Number[]](../../guide/types/#number)  
A list or array of numbers on which to perform the operation.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints 5

```arcade
var values = [0,5,10]
Average(values)
```


<a name="average2"></a>
### Average( features, fieldNameOrSQLExpression ) -> [Number](../../guide/types/#number)

Returns the average value of a given numeric field in a [FeatureSet](../../guide/types/#featureset).

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
A FeatureSet on which to perform the operation.
- **`fieldNameOrSQLExpression`**: [Text](../../guide/types/#text)  
Specifies the name of a numeric field or SQL92 expression for which the statistic will be calculated from the input FeatureSet.

#### Return value: [Number](../../guide/types/#number)

#### Example

calculates the difference between the feature's population and the average population of all features in the layer

```arcade
$feature.population - Average($layer, 'population')
```

calculates the average population per square mile of all features in the layer

```arcade
Average($layer, 'population / area')
```


---------------------

## Ceil

### Ceil( value, numPlaces? ) -> [Number](../../guide/types/#number)

Returns the input value rounded upwards to the given number of decimal places.

#### Parameters

- **`value`**: [Number](../../guide/types/#number)  
The number to round upward.
- **`numPlaces`** (_Optional_): [Number](../../guide/types/#number)  
The number of decimal places to round the `value` to. Default is 0. Trailing zeros will be truncated.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints 2135.1

```arcade
Ceil(2135.0905, 2)
```


---------------------

## Constrain

### Constrain( value, lowerBound, upperBound ) -> [Number](../../guide/types/#number)

**[Since version 1.2](../../guide/version-matrix)**

Constrains the given input `value` to minimum and maximum bounds. For example, if the input value is `10`, the lower bound is `50`, and the upper bound is `100`, then `50` is returned.

#### Parameters

- **`value`**: [Number](../../guide/types/#number)  
The value to constrain to the given `min` and `max` bounds.
- **`lowerBound`**: [Number](../../guide/types/#number)  
The lower bound by which to constrain the input `value`. If the given value is less than the `min`, then `min` is returned.
- **`upperBound`**: [Number](../../guide/types/#number)  
The upper bound by which to constrain the input `value`. If the given value is greater than the `max`, then `max` is returned.

#### Return value: [Number](../../guide/types/#number)

#### Example

returns 5

```arcade
Constrain(5, 0, 10)
```

returns 0

```arcade
Constrain(-3, 0, 10)
```

returns 10

```arcade
Constrain(553, 0, 10)
```


---------------------

## Cos

### Cos( value ) -> [Number](../../guide/types/#number)

Returns the cosine of the input value in radians.

#### Parameters

- **`value`**: [Number](../../guide/types/#number)  
A number in radians on which to perform the operation.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints 0.540302

```arcade
Cos(1)
```


---------------------

## Exp

### Exp( x ) -> [Number](../../guide/types/#number)

Returns the value of e to the power of x, where e is the base of the natural logarithm `2.718281828`.

#### Parameters

- **`x`**: [Number](../../guide/types/#number)  
The power, or number of times to multiply `e` to itself.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints 7.389056

```arcade
Exp(2)
```


---------------------

## Floor

### Floor( value, numPlaces? ) -> [Number](../../guide/types/#number)

Returns the input value rounded downward to the given number of decimal places.

#### Parameters

- **`value`**: [Number](../../guide/types/#number)  
A number to round downward.
- **`numPlaces`** (_Optional_): [Number](../../guide/types/#number)  
The number of decimal places to round the number. Default is 0. Trailing zeros will be truncated.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints 2316.25

```arcade
Floor(2316.2562, 2)
```


---------------------

## Log

### Log( x ) -> [Number](../../guide/types/#number)

Returns the natural logarithm (base e) of x.

#### Parameters

- **`x`**: [Number](../../guide/types/#number)  
A number on which to perform the operation.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints 2.302585

```arcade
Log(10)
```


---------------------

## Max

This function has 2 signatures:

- [Max( numbers ) -> Number](#max1)
- [Max( features, fieldNameOrSQLExpression ) -> Number](#max2)

<a name="max1"></a>
### Max( numbers ) -> [Number](../../guide/types/#number)

Returns the highest value from an array of numbers.

#### Parameters

- **`numbers`**: [Number[]](../../guide/types/#number)  
An array or list of numbers.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints 89

```arcade
Max([23,56,89])
```

prints 120

```arcade
Max(23,5,120,43,9)
```


<a name="max2"></a>
### Max( features, fieldNameOrSQLExpression ) -> [Number](../../guide/types/#number)

Returns the highest value for a given numeric field from a [FeatureSet](../../guide/types/#featureset).

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
A FeatureSet on which to perform the operation.
- **`fieldNameOrSQLExpression`**: [Text](../../guide/types/#text)  
Specifies the name of a numeric field or SQL92 expression for which the statistic will be calculated from the input FeatureSet.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints the max value of the population field for all features in the layer

```arcade
Max($layer, 'population')
```

calculates the max population per square mile of all features in the layer

```arcade
Max($layer, 'population / area')
```


---------------------

## Mean

This function has 2 signatures:

- [Mean( numbers ) -> Number](#mean1)
- [Mean( features, fieldNameOrSQLExpression ) -> Number](#mean2)

<a name="mean1"></a>
### Mean( numbers ) -> [Number](../../guide/types/#number)

**[Since version 1.1](../../guide/version-matrix)**

Returns the mean value of an array of numbers.

#### Parameters

- **`numbers`**: [Number[]](../../guide/types/#number)  
A list or array of numbers from which to calculate the mean.

#### Return value: [Number](../../guide/types/#number)

#### Example

Use a single array as input.

```arcade
var values = [1,2,3,4,5,6,7,8,9];
Mean(values);
// returns 5
```

Use comma separated values with array element.

```arcade
var values = [0,10];
Mean(0,10,5,values);
// returns 5
```


<a name="mean2"></a>
### Mean( features, fieldNameOrSQLExpression ) -> [Number](../../guide/types/#number)

**[Since version 1.1](../../guide/version-matrix)**

Returns the mean value of a given numeric field in a [FeatureSet](../../guide/types/#featureset).

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
A FeatureSet on which to calculate the mean.
- **`fieldNameOrSQLExpression`**: [Text](../../guide/types/#text)  
Specifies the name of a numeric field or SQL92 expression for which the statistic will be calculated from the input FeatureSet.

#### Return value: [Number](../../guide/types/#number)

#### Example

calculates the difference between the feature's population and the mean population of all features in the layer

```arcade
$feature.population - Mean($layer, 'population')
```

calculates the mean population per square mile of all features in the layer

```arcade
Mean($layer, 'population / area')
```


---------------------

## Min

This function has 2 signatures:

- [Min( numbers ) -> Number](#min1)
- [Min( features, fieldNameOrSQLExpression ) -> Number](#min2)

<a name="min1"></a>
### Min( numbers ) -> [Number](../../guide/types/#number)

Returns the lowest value in a given array.

#### Parameters

- **`numbers`**: [Number[]](../../guide/types/#number)  
An array or list of numbers.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints 23

```arcade
Min([23,56,89])
```

prints 5

```arcade
Min(23,5,120,43,9)
```


<a name="min2"></a>
### Min( features, fieldNameOrSQLExpression ) -> [Number](../../guide/types/#number)

Returns the lowest value for a given numeric field from a [FeatureSet](../../guide/types/#featureset).

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
A FeatureSet on which to perform the operaiton.
- **`fieldNameOrSQLExpression`**: [Text](../../guide/types/#text)  
Specifies the name of a numeric field or SQL92 expression for which the statistic will be calculated from the input FeatureSet.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints the min value of the population field for all features in the layer

```arcade
Min($layer, 'population')
```

returns the minimum population per square mile of all features in the layer

```arcade
Min($layer, 'population / area')
```


---------------------

## Pow

### Pow( x, y ) -> [Number](../../guide/types/#number)

Returns the value of x to the power of y.

#### Parameters

- **`x`**: [Number](../../guide/types/#number)  
The base value.
- **`y`**: [Number](../../guide/types/#number)  
The exponent. This indicates the number of times to multiply `x` by itself.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints 9

```arcade
Pow(3, 2)
```


---------------------

## Random

### Random(  ) -> [Number](../../guide/types/#number)

Returns a random number between 0 and 1.

#### Return value: [Number](../../guide/types/#number)

#### Example

```arcade
Random()
```


---------------------

## Round

### Round( value, numPlaces? ) -> [Number](../../guide/types/#number)

Returns the input value, rounded to the given number of decimal places.  
_Note: If you're looking to format a value for display in a label or popup, use the [text](../data_functions/#text) function._

#### Parameters

- **`value`**: [Number](../../guide/types/#number)  
A number to round.
- **`numPlaces`** (_Optional_): [Number](../../guide/types/#number)  
The number of decimal places to round the number to. Default is `0`. Trailing zeros will be truncated.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints 2316.26

```arcade
Round(2316.2562, 2)
```


---------------------

## Sin

### Sin( value ) -> [Number](../../guide/types/#number)

Returns the sine of the input value.

#### Parameters

- **`value`**: [Number](../../guide/types/#number)  
A number in radians on which to perform the operation.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints 0.841741

```arcade
Sin(1)
```


---------------------

## Sqrt

### Sqrt( value ) -> [Number](../../guide/types/#number)

Returns the square root of a number.

#### Parameters

- **`value`**: [Number](../../guide/types/#number)  
A number on which to calculate the square root.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints 3

```arcade
Sqrt(9)
```


---------------------

## Stdev

This function has 2 signatures:

- [Stdev( numbers ) -> Number](#stdev1)
- [Stdev( features, fieldNameOrSQLExpression ) -> Number](#stdev2)

<a name="stdev1"></a>
### Stdev( numbers ) -> [Number](../../guide/types/#number)

Returns the standard deviation (population standard deviation) of a set of numbers.

#### Parameters

- **`numbers`**: [Number[]](../../guide/types/#number)  
An array or list of numbers on which to perform the operation.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints 27.5

```arcade
Stdev(23,56,89,12,45,78)
```


<a name="stdev2"></a>
### Stdev( features, fieldNameOrSQLExpression ) -> [Number](../../guide/types/#number)

Returns the standard deviation for the values from a given numeric field in a [FeatureSet](../../guide/types/#featureset).

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
A FeatureSet on which to perform the operation.
- **`fieldNameOrSQLExpression`**: [Text](../../guide/types/#text)  
Specifies the name of a numeric field or SQL92 expression for which the statistic will be calculated from the input FeatureSet.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints the standard deviation of values from the 'population' field

```arcade
Stdev($layer, 'population')
```

calculates the standard deviation of the population per square mile of all features in the layer

```arcade
Stdev($layer, 'population / area')
```


---------------------

## Sum

This function has 2 signatures:

- [Sum( numbers ) -> Number](#sum1)
- [Sum( features, fieldNameOrSQLExpression ) -> Number](#sum2)

<a name="sum1"></a>
### Sum( numbers ) -> [Number](../../guide/types/#number)

Returns the sum of a set of numbers.

#### Parameters

- **`numbers`**: [Number[]](../../guide/types/#number)  
An array of numbers on which to perform the operation.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints 303

```arcade
Sum(23,56,89,12,45,78)
```


<a name="sum2"></a>
### Sum( features, fieldNameOrSQLExpression ) -> [Number](../../guide/types/#number)

Returns the sum of values returned from a given numeric field in a [FeatureSet](../../guide/types/#featureset).

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
A FeatureSet on which to perform the operation.
- **`fieldNameOrSQLExpression`**: [Text](../../guide/types/#text)  
Specifies the name of a numeric field or SQL92 expression for which the statistic will be calculated from the input FeatureSet.

#### Return value: [Number](../../guide/types/#number)

#### Example

calculates the population of the current feature as a % of the total population of all features in the layer

```arcade
( $feature.population / Sum($layer, 'population') ) * 100
```

calculates the total number of votes cast in an election for the entire dataset

```arcade
Sum($layer, 'democrat + republican + other')
```


---------------------

## Tan

### Tan( value ) -> [Number](../../guide/types/#number)

Returns the tangent of an angle in radians.

#### Parameters

- **`value`**: [Number](../../guide/types/#number)  
A number on which to calculate the tangent.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints 0.57389

```arcade
Tan(0.521)
```


---------------------

## Variance

This function has 2 signatures:

- [Variance( numbers ) -> Number](#variance1)
- [Variance( features, fieldNameOrSQLExpression ) -> Number](#variance2)

<a name="variance1"></a>
### Variance( numbers ) -> [Number](../../guide/types/#number)

Returns the variance (population variance) of a set of numbers.

#### Parameters

- **`numbers`**: [Number[]](../../guide/types/#number)  
An array of numbers on which to perform the operation.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints 756.25

```arcade
Variance(12,23,45,56,78,89)
```


<a name="variance2"></a>
### Variance( features, fieldNameOrSQLExpression ) -> [Number](../../guide/types/#number)

Returns the variance of the values from a given numeric field in a [FeatureSet](../../guide/types/#featureset).

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
A FeatureSet on which to perform the operation.
- **`fieldNameOrSQLExpression`**: [Text](../../guide/types/#text)  
Specifies the name of a numeric field or SQL92 expression for which the statistic will be calculated from the input FeatureSet.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints the variance for the population field in the given layer

```arcade
Variance($layer, 'population')
```

calculates the variance of the population per square mile of all features in the layer

```arcade
Variance($layer, 'population / area')
```


---------------------