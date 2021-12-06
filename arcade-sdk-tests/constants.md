---
title: Constants
description: Documentation for all Constants supported in Arcade.
keywords:
  - Infinity
  - PI
  - TextFormatting.BackwardSlash
  - TextFormatting.DoubleQuote
  - TextFormatting.ForwardSlash
  - TextFormatting.NewLine
  - TextFormatting.SingleQuote
---

# Constants

The following constants are available for your convenience in writing expressions.

---------------------

## Infinity

Represents a value greater than any other number. `-Infinity` may also be used as a value smaller than any number.

#### Example

Calculates the maximum of four field values

```arcade
var values = [ $feature.field1, $feature.field2, $feature.field3, $feature.field4 ];
var maxValue = -Infinity;

for(var i in values){
  maxValue = IIF(values[i] > maxValue, values[i], maxValue);
}

return maxValue;
```


---------------------

## PI

The value of a circle's circumference divided by its diameter, approximately `3.14159`.

#### Example

Returns the area of a circle feature

```arcade
var r = $feature.radius;
PI * r * r;
```


---------------------

## TextFormatting.BackwardSlash

Inserts a backslash character `\` into the text.

#### Example

Returns '\\\serverName\foo\bar'

```arcade
TextFormatting.BackwardSlash + TextFormatting.BackwardSlash + $feature.FILE_PATH
```


---------------------

## TextFormatting.DoubleQuote

Inserts a double quote character `"` into the text.

#### Example

Returns 'Nicholas "Nick" Anderson'

```arcade
$feature.NAME + " " + TextFormatting.DoubleQuote + $feature.ALIAS + TextFormatting.DoubleQuote + " " + $feature.SURNAME
```


---------------------

## TextFormatting.ForwardSlash

Inserts a forward slash character `/` into the text.

#### Example

Returns '151/low'

```arcade
$feature.POP_DENSITY + TextFormatting.ForwardSlash + $feature.CLASS
```


---------------------

## TextFormatting.NewLine

Inserts a new line, or line break, into the text. Multi-line labels are **NOT** supported in the ArcGIS API 3.x for JavaScript nor in the ArcGIS Online map viewer.

#### Example

Returns "T2N
R1W"

```arcade
"T" + $feature.TOWNSHIP + TextFormatting.NewLine + "R" + $feature.RANGE
```


---------------------

## TextFormatting.SingleQuote

Inserts a single quote character `'` into the text.

#### Example

Returns "Nicholas 'Nick' Anderson"

```arcade
$feature.NAME + " " + TextFormatting.SingleQuote + $feature.ALIAS + TextFormatting.SingleQuote + " " + $feature.SURNAME
```


---------------------