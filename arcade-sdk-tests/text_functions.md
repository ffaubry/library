---
title: Text Functions
description: Documentation for all Text Functions supported in Arcade.
keywords:
  - Concatenate
  - Find
  - FromCharCode
  - FromCodePoint
  - Left
  - Lower
  - Mid
  - Proper
  - Replace
  - Right
  - Split
  - Text
  - ToCharCode
  - ToCodePoint
  - Trim
  - Upper
  - UrlEncode
---

# Text Functions

Functions for formatting text values. These are commonly used in the labeling and popup profiles.

---------------------

## Concatenate

### Concatenate( textArray, separator?, format? ) -> [Text](../../guide/types/#text)

Concatenates values together and returns a text value.

#### Parameters

- **`textArray`**: [Text[]](../../guide/types/#text)  
An array of text values to concatenate.
- **`separator`** (_Optional_): [Text](../../guide/types/#text)  
Separator to use for concatenation if `values` parameter is an array. Or text to concatenate, if a single value is provided for the first parameter. If not provided will be empty.
- **`format`** (_Optional_): [Text](../../guide/types/#text)  
Formatting text for dates or numbers. This parameter is available in Arcade version 1.3 and later. See the list of possible values below.

| **Value** | **Description** |
| :--- | :--- |
| 0 | Digit |
| # | Digit, omitting leading/trailing zeros |
| D | Day of the month, not padded (1 - 31) |
| DD | Day of the month, padded (01 - 31) |
| DDD | Ordinal day of the year (1 - 365) |
| d | Day of the week (1 - 7) |
| ddd | Abbreviated day of the week (e.g. Mon) |
| dddd | Full day of the week (e.g. Monday) |
| M | Month number (1 - 12) |
| MM | Month number, padded (01 - 12) |
| MMM | Abbreviated month name (e.g. Jan) |
| MMMM | Full month name (e.g. January) |
| m | Minutes, not padded (0 - 59) |
| mm | Minutes, padded (00 - 59) |
| Y | Full year |
| YY | Two-digit year |
| h | Civilian hours, not padded (0 - 12) |
| hh | Civilian hours, padded (00 - 12) |
| H | Military hours, not padded (0 - 24) |
| HH | Military hours, padded (00 - 24) |
| s | Seconds, not padded (0 - 59) |
| ss | Seconds, padded (00 - 59) |


#### Return value: [Text](../../guide/types/#text)

#### Example

prints 'red/blue/green'

```arcade
Concatenate(['red', 'blue', 'green'], '/')
```


---------------------

## Find

### Find( searchText, targetText, startpos? ) -> [Number](../../guide/types/#number)

Finds a string of characters within a text value. Wildcards are NOT supported. A returned value of `-1` indicates no results were found.

#### Parameters

- **`searchText`**: [Text](../../guide/types/#text)  
The character string to search for.
- **`targetText`**: [Text](../../guide/types/#text)  
The text to search.
- **`startpos`** (_Optional_): [Number](../../guide/types/#number)  
The zero-based index of the location in the text to search from.

#### Return value: [Number](../../guide/types/#number)

#### Example

prints 6

```arcade
Find('380', 'Esri, 380 New York Street', 0)
```


---------------------

## FromCharCode

### FromCharCode( charCode1, [charCode2, ..., charCodeN]? ) -> [Text](../../guide/types/#text)

**[Since version 1.16](../../guide/version-matrix)**

Returns a text value created from a sequence of UTF-16 character codes.

#### Parameters

- **`charCode1`**: [Number](../../guide/types/#number)  
A number representing UTF-16 code units. Each unit has a range of 0-65535.
- **`[charCode2, ..., charCodeN]`** (_Optional_): [Number](../../guide/types/#number)  
Ongoing sequence of numbers representing UTF-16 code units. Each unit has a range of 0-65535.

#### Return value: [Text](../../guide/types/#text)

#### Example

The following example returns 'XYZ'

```arcade
FromCharCode(88,89,90)
// returns 'XYZ'
```

The following example returns '🌉'

```arcade
FromCharCode(55356, 57097)
// returns '🌉'
```


---------------------

## FromCodePoint

### FromCodePoint( codePoint1, [codePoint2, ..., codePoint1N]? ) -> [Text](../../guide/types/#text)

**[Since version 1.16](../../guide/version-matrix)**

Returns a text value created from a sequence of UTF-32 code points.

#### Parameters

- **`codePoint1`**: [Number](../../guide/types/#number)  
A code point.
- **`[codePoint2, ..., codePoint1N]`** (_Optional_): [Number](../../guide/types/#number)  
A list of code points

#### Return value: [Text](../../guide/types/#text)

#### Example

The following example returns 'XYZ'

```arcade
FromCodePoint(88,89,90)
// returns 'XYZ'
```

The following example returns '🌉'

```arcade
FromCodePoint(127753)
// returns '🌉'
```


---------------------

## Left

### Left( value, charCount ) -> [Text](../../guide/types/#text)

Returns the specified number of characters from the beginning of a text value.

#### Parameters

- **`value`**: [Text](../../guide/types/#text) \| [Array](../../guide/types/#array) \| [Number](../../guide/types/#number) \| [Boolean](../../guide/types/#boolean)  
The value from which to get characters.
- **`charCount`**: [Number](../../guide/types/#number)  
The number of characters to get from the beginning of the text.

#### Return value: [Text](../../guide/types/#text)

#### Example

prints 'the'

```arcade
Left('the quick brown fox', 3)
```


---------------------

## Lower

### Lower( text ) -> [Text](../../guide/types/#text)

Makes a text value lower case.

#### Parameters

- **`text`**: [Text](../../guide/types/#text)  
The text to be made lowercase.

#### Return value: [Text](../../guide/types/#text)

#### Example

prints 'hello'

```arcade
Lower('HELLO')
```


---------------------

## Mid

### Mid( value, startpos, charCount ) -> [Text](../../guide/types/#text)

Gets a number of characters from the middle of a text value.

#### Parameters

- **`value`**: [Text](../../guide/types/#text) \| [Array](../../guide/types/#array) \| [Number](../../guide/types/#number) \| [Boolean](../../guide/types/#boolean)  
The value from which to get characters.
- **`startpos`**: [Number](../../guide/types/#number)  
The starting position from which to get the text. 0 is the first position.
- **`charCount`**: [Number](../../guide/types/#number)  
The number of characters to extract.

#### Return value: [Text](../../guide/types/#text)

#### Example

prints 'quick'

```arcade
Mid('the quick brown fox', 4, 5)
```


---------------------

## Proper

### Proper( text, applyToText ) -> [Text](../../guide/types/#text)

Converts a text value to title case. By default, the beginning of every word is capitalized. The option `firstword` will capitalize only the first word.

#### Parameters

- **`text`**: [Text](../../guide/types/#text)  
The text to convert to title case.
- **`applyToText`**: [Text](../../guide/types/#text)  
A text value specifying the type of capitalization to be performed. By default every word is capitalized. This parameter accepts one of two values: `everyword` or `firstword`.

#### Return value: [Text](../../guide/types/#text)

#### Example

prints 'The Quick Brown Fox'

```arcade
Proper('the quick brown fox', 'everyword')
```


---------------------

## Replace

### Replace( value, searchText, replacementText, allOccurrences? ) -> [Text](../../guide/types/#text)

Replaces a string within a text value or an element within an array. Defaults to replacing all occurrences.

#### Parameters

- **`value`**: [Text](../../guide/types/#text) \| [Array](../../guide/types/#array) \| [Number](../../guide/types/#number) \| [Boolean](../../guide/types/#boolean)  
The value in which to make replacements.
- **`searchText`**: [Text](../../guide/types/#text)  
The text to search for.
- **`replacementText`**: [Text](../../guide/types/#text)  
The replacement text.
- **`allOccurrences`** (_Optional_): [Boolean](../../guide/types/#boolean)  
Indicates if all occurrences of the `searchText` should be replaced in the text. Defaults to `true`.

#### Return value: [Text](../../guide/types/#text)

#### Example

prints 'the quick red fox'

```arcade
Replace('the quick brown fox', 'brown', 'red')
```


---------------------

## Right

### Right( value, charCount ) -> [Text](../../guide/types/#text)

Returns the specified number of characters from the end of a text value.

#### Parameters

- **`value`**: [Text](../../guide/types/#text) \| [Array](../../guide/types/#array) \| [Number](../../guide/types/#number) \| [Boolean](../../guide/types/#boolean)  
The text from which to get characters.
- **`charCount`**: [Number](../../guide/types/#number)  
The number of characters to get from the end of the text value.

#### Return value: [Text](../../guide/types/#text)

#### Example

prints 'fox'

```arcade
Right('the quick brown fox', 3)
```


---------------------

## Split

### Split( text, separatorText, limit?, removeEmpty? ) -> [Text[]](../../guide/types/#text)

Splits a text value into an array.

#### Parameters

- **`text`**: [Text](../../guide/types/#text)  
The text value to be split.
- **`separatorText`**: [Text](../../guide/types/#text)  
The separator used to split the text.
- **`limit`** (_Optional_): [Number](../../guide/types/#number)  
An integer that specifies the number of splits. The default is `-1`, which indicates an unlimited number of splits.
- **`removeEmpty`** (_Optional_): [Boolean](../../guide/types/#boolean)  
Indicates whether to remove empty values. By default this is `false`.

#### Return value: [Text[]](../../guide/types/#text)

#### Example

returns '[red,green]'

```arcade
Split('red,green,blue,orange', ',', 2)
```

Splits the paragraph at each space an unlimited number of times. Returns an array of the words in the paragraph.

```arcade
Split(paragraph, ' ', -1, true)
```


---------------------

## Text

### Text( value, format? ) -> [Text](../../guide/types/#text)

Converts its argument into a string and optionally formats it. Returns `null` if it fails.

#### Parameters

- **`value`**: *  
A value to be converted to a string (e.g. date, number or other type). When a date is provided, this function assumes the date/time object is in UTC and automatically converts the value to the local time of the client executing the expression. If the date/time value returned from the database already represents local time, then you should use the `toUTC` function to avoid applying an extra offset.
- **`format`** (_Optional_): [Text](../../guide/types/#text)  
Formatting string for dates or numbers. See the list of possible values below.

| **Value** | **Description** |
| :--- | :--- |
| 0 | Digit |
| # | Digit, omitting leading/trailing zeros |
| D | Day of the month, not padded (1 - 31) |
| DD | Day of the month, padded (01 - 31) |
| DDD | Ordinal day of the year (1 - 365) |
| d | Day of the week (1 - 7) |
| ddd | Abbreviated day of the week (e.g. Mon) |
| dddd | Full day of the week (e.g. Monday) |
| M | Month number (1 - 12) |
| MM | Month number, padded (01 - 12) |
| MMM | Abbreviated month name (e.g. Jan) |
| MMMM | Full month name (e.g. January) |
| m | Minutes, not padded (0 - 59) |
| mm | Minutes, padded (00 - 59) |
| Y | Full year |
| YY | Two-digit year |
| h | Civilian hours, not padded (0 - 12) |
| hh | Civilian hours, padded (00 - 12) |
| H | Military hours, not padded (0 - 24) |
| HH | Military hours, padded (00 - 24) |
| s | Seconds, not padded (0 - 59) |
| ss | Seconds, padded (00 - 59) |


#### Return value: [Text](../../guide/types/#text)

#### Example

Pad the number to the left of the decimal

```arcade
Text(123, '0000') // '0123'
```

Restrict the number to the left of the decimal

```arcade
Text(123, '00') // '23'
```

Group the number by thousands

```arcade
Text(1234, '#,###') // '1,234'
```

Round the number to two decimal places

```arcade
Text(12345678.123, '#,###.00') // '12,345,678.12'
```

Format number as currency

```arcade
Text(1234.55, '$#,###.00') // '$1,234.55'
```

Round the number to two decimal places

```arcade
Text(1.236, '#.00') // '1.24'
```

Maintain significant digits and group by thousands

```arcade
Text(1234.5678, '#,##0.00#') // '1,234.568'
```

Format the number and format positive/negative - if there is a negative subpattern, it serves only to specify the negative prefix and suffix

```arcade
Text(-2, 'Floor #;Basement #') // 'Basement 2'
```

```arcade
Text(2, 'Floor #;Basement #') // 'Floor 2'
```

Multiply by 100 and format as percentage

```arcade
Text(0.3, '#%') // '30%'
```

Format date and time at the moment. eg 'Tuesday, October 25, 2016 @ 08:43:11'

```arcade
Text(Now(), 'dddd, MMMM D, Y @ h:m:s')
```

Date stored in the `datetime` field already represents local time, but Arcade assumes it is UTC. Offsets the local time to UTC to avoid applying the timezone offset twice.

```arcade
Text(ToUTC($feature.datetime), 'dddd, MMMM D, Y @ h:m:s')
```


---------------------

## ToCharCode

### ToCharCode( text, index? ) -> [Number](../../guide/types/#number)

**[Since version 1.16](../../guide/version-matrix)**

Returns a number between 0 and 65535 representing the UTF-16 code unit at the given index. Invalid halves of surrogate pairs are automatically removed.

#### Parameters

- **`text`**: [Text](../../guide/types/#text)  
The text from which to get a UTF-16 code unit value.
- **`index`** (_Optional_): [Number](../../guide/types/#number)  
An integer with a value of at least 0 and no greater than the number of characters of `inputText`. By default, this value is 0.

#### Return value: [Number](../../guide/types/#number)

#### Example

The following example returns 88, the Unicode value for X.

```arcade
ToCharCode('XYZ')
// returns 88
```

The following example returns 89, the Unicode value for Y.

```arcade
ToCharCode('XYZ', 1)
// returns 89
```

The following example returns 65535.

```arcade
ToCharCode('\uFFFF\uFFFE')
// returns 65535
```

The following example returns 55356.

```arcade
ToCharCode('🌉')
// returns 55356
```

The following example returns 57097.

```arcade
ToCharCode('🌉', 1)
// returns 57097
```


---------------------

## ToCodePoint

### ToCodePoint( text, position? ) -> [Number](../../guide/types/#number)

**[Since version 1.16](../../guide/version-matrix)**

Returns a non-negative number representing the UTF-32 code point value of the input text. If indexed into the first half of a surrogate pair, the whole code point is returned. If indexed into the second half of the pair, this function returns the value of the second half. If a large code isn't a valid character, the function returns only the value of the half it indexes into.

#### Parameters

- **`text`**: [Text](../../guide/types/#text)  
The text from which to get a UTF-32 code point value.
- **`position`** (_Optional_): [Number](../../guide/types/#number)  
Position of a character in `inputText` from which to return the code point value. By default this value is 0.

#### Return value: [Number](../../guide/types/#number)

#### Example

The following example returns 88, the Unicode value for X.

```arcade
ToCodePoint('XYZ')
// returns 88
```

The following example returns 89, the Unicode value for Y.

```arcade
ToCodePoint('XYZ', 1)
// returns 89
```

The following example returns 127753.

```arcade
ToCodePoint('🌉')
// returns 127753
```

The following example returns 57097.

```arcade
ToCodePoint('🌉', 1)
// returns 57097
```


---------------------

## Trim

### Trim( text ) -> [Text](../../guide/types/#text)

Removes spaces from the beginning or end of an input text value.

#### Parameters

- **`text`**: [Text](../../guide/types/#text)  
The text to be trimmed.

#### Return value: [Text](../../guide/types/#text)

#### Example

prints 'hello world'

```arcade
Trim('   hello world')
```


---------------------

## Upper

### Upper( text ) -> [Text](../../guide/types/#text)

Makes text upper case.

#### Parameters

- **`text`**: [Text](../../guide/types/#text)  
The text value to be made uppercase.

#### Return value: [Text](../../guide/types/#text)

#### Example

prints 'HELLO'

```arcade
Upper('Hello')
```


---------------------

## UrlEncode

### UrlEncode( textOrDictionary ) -> [Text](../../guide/types/#text)

**[Since version 1.7](../../guide/version-matrix)**

Encodes a URL by replacing each instance of certain characters by one, two, three, or four escape sequences representing the UTF-8 encoding of the character.

#### Parameters

- **`textOrDictionary`**: [Text](../../guide/types/#text) \| [Dictionary](../../guide/types/#dictionary)  
The URL to be encoded.

#### Return value: [Text](../../guide/types/#text)

#### Example

Encodes the URL provided

```arcade
var urlsource ='arcgis-survey123://?';
var params = {
  itemID:'36ff9e8c13e042a58cfce4ad87f55d19',
  center: '43.567,-117.380'
};
return urlsource  + UrlEncode(params);
//arcgis-survey123://?center=43.567%2C-117.380&itemID=36ff9e8c13e042a58cfce4ad87f55d19
```


---------------------