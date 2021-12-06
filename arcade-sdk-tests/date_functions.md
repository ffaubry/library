---
title: Date Functions
description: Documentation for all Date Functions supported in Arcade.
keywords:
  - Date
  - DateAdd
  - DateDiff
  - Day
  - Hour
  - ISOMonth
  - ISOWeek
  - ISOWeekday
  - ISOYear
  - Millisecond
  - Minute
  - Month
  - Now
  - Second
  - Timestamp
  - Today
  - ToLocal
  - ToUTC
  - Week
  - Weekday
  - Year
---

# Date Functions

The Date functions provide methods for creating date objects and getting various properties of the objects. The [DateAdd()](#dateadd) and [DateDiff()](#datediff) functions are convenient for adjusting the desired date based on a specified interval. The [Now()](#now) function may also be used to get the current time in the local time of the client.

---------------------

## Date

This function has 3 signatures:

- [Date( year, month, day, hour?, minute?, second?, millisecond? ) -> Date](#date1)
- [Date( epoch? ) -> Date](#date2)
- [Date( timestamp? ) -> Date](#date3)

<a name="date1"></a>
### Date( year, month, day, hour?, minute?, second?, millisecond? ) -> [Date](../../guide/types/#date)

Parses a value or set of values to a Date object. Dates that are manually created are assumed to be UTC. See the example snippets below to view various ways this function may be used.

#### Parameters

- **`year`**: [Number](../../guide/types/#number)  
A number representing a year.
- **`month`**: [Number](../../guide/types/#number)  
The month (0-11) where `0` is January and `11` is December.
- **`day`**: [Number](../../guide/types/#number)  
The day of the month (1-31).
- **`hour`** (_Optional_): [Number](../../guide/types/#number)  
The hour of the day (0-23).
- **`minute`** (_Optional_): [Number](../../guide/types/#number)  
The minute of the hour (0-59).
- **`second`** (_Optional_): [Number](../../guide/types/#number)  
The second of the minute (0-59).
- **`millisecond`** (_Optional_): [Number](../../guide/types/#number)  
The millisecond of the second (0-999).

#### Return value: [Date](../../guide/types/#date)

#### Example

Year, month, day

```arcade
Date(1987,05,02) // 'Tue Jun 02 1987 00:00:00 GMT-0700 (PDT)'
```

Prints the current date and time

```arcade
Date()
```


<a name="date2"></a>
### Date( epoch? ) -> [Date](../../guide/types/#date)

Converts a Unix epoch number to a Date object.

#### Parameters

- **`epoch`** (_Optional_): [Number](../../guide/types/#number)  
The number of milliseconds since January 1, 1970 UTC.

#### Return value: [Date](../../guide/types/#date)

#### Example

Returns a date object based on a field value

```arcade
var recordDate = Date($feature.dateField)
```

Milliseconds since epoch

```arcade
Date(1476987783555) // 'Thu Oct 20 2016 11:23:03 GMT-0700 (PDT)'
```


<a name="date3"></a>
### Date( timestamp? ) -> [Date](../../guide/types/#date)

Converts an ISO 8601 string to a Date object.

#### Parameters

- **`timestamp`** (_Optional_): [Text](../../guide/types/#text)  
An ISO 8601 string to be converted into a date.

#### Return value: [Date](../../guide/types/#date)

#### Example

ISO 8601 string

```arcade
Date('2016-10-20T17:41:37+00:00') // 'Thu Oct 20 2016 10:41:37 GMT-0700 (PDT)'
```


---------------------

## DateAdd

### DateAdd( date, addValue, units ) -> [Date](../../guide/types/#date)

Adds a specified amount of time in the given units to a date and returns a new date.

#### Parameters

- **`date`**: [Date](../../guide/types/#date)  
The input date to which to add time.
- **`addValue`**: [Number](../../guide/types/#number)  
The value to add to the date in the given units.
- **`units`**: [Text](../../guide/types/#text)  
The units of the number to add to the date. The supported unit types include `milliseconds`, `seconds`, `minutes`, `hours`, `days`, `months`, `years`

#### Return value: [Date](../../guide/types/#date)

#### Example

Adds 7 days to the date in the provided field

```arcade
var startDate = Date($feature.dateField);
var oneWeekLater = DateAdd(startDate, 7, 'days');
return oneWeekLater;
```


---------------------

## DateDiff

### DateDiff( date1, date2, units? ) -> [Number](../../guide/types/#number)

Subtracts two dates, and returns the difference in the specified units.

#### Parameters

- **`date1`**: [Date](../../guide/types/#date)  
The date value from which to subtract a second date.
- **`date2`**: [Date](../../guide/types/#date)  
The date value to subtract from the first given date.
- **`units`** (_Optional_): [Text](../../guide/types/#text)  
The units in which to return the difference of the two given dates. The supported unit types include `milliseconds`, `seconds`, `minutes`, `hours`, `days`, `months`, `years`. The default value is `milliseconds`.

#### Return value: [Number](../../guide/types/#number)

#### Example

Subtracts two dates and returns the age

```arcade
var startDate = Date($feature.startDateField);
var endDate = Date($feature.endDateField);
var age = DateDiff(endDate, startDate, 'years');
return age;
```


---------------------

## Day

### Day( date ) -> [Number](../../guide/types/#number)

Returns the day of the month of the given date.

#### Parameters

- **`date`**: [Date](../../guide/types/#date)  
A date value from which to get the day of the month.

#### Return value: [Number](../../guide/types/#number)

#### Example

Gets the day of the month of the current date

```arcade
Day(Now())
```


---------------------

## Hour

### Hour( date ) -> [Number](../../guide/types/#number)

Returns the hour of the time in the given date (0-23).

#### Parameters

- **`date`**: [Date](../../guide/types/#date)  
A date value from which to get the hour of the time.

#### Return value: [Number](../../guide/types/#number)

#### Example

Gets the hour of the current time

```arcade
Hour(Now())
```


---------------------

## ISOMonth

### ISOMonth( date ) -> [Number](../../guide/types/#number)

**[Since version 1.12](../../guide/version-matrix)**

Returns the month of the given date, based on the ISO 8601 standard. Values range from 1-12 where January is `1` and December is `12`.

#### Parameters

- **`date`**: [Date](../../guide/types/#date)  
A date value from which to get the month.

#### Return value: [Number](../../guide/types/#number)

#### Example

Gets the month of the given date, based on the ISO 8601 standard. Returns `12`, for the month of December.

```arcade
ISOMonth(Date(1980, 11, 31))
```


---------------------

## ISOWeek

### ISOWeek( date ) -> [Number](../../guide/types/#number)

**[Since version 1.12](../../guide/version-matrix)**

Returns the week in the year of the given date, based on the ISO 8601 week date calendar. Values range from 1-53 where the first week of the year is `1` and the last week of the year is `52` or `53`, depending on the year.

#### Parameters

- **`date`**: [Date](../../guide/types/#date)  
A date value from which to get the week.

#### Return value: [Number](../../guide/types/#number)

#### Example

Gets the week of the given date, based on the ISO 8601 standard. Returns `1`, since this date is included in the first week of the following year.

```arcade
ISOWeek(Date(1980, 11, 31))
```


---------------------

## ISOWeekday

### ISOWeekday( date ) -> [Number](../../guide/types/#number)

**[Since version 1.12](../../guide/version-matrix)**

Returns the day of the week of the given date, based on the ISO 8601 standard. Values range from 1-7 where Monday is `1` and Sunday is `7`.

#### Parameters

- **`date`**: [Date](../../guide/types/#date)  
A date value from which to return the day of the week.

#### Return value: [Number](../../guide/types/#number)

#### Example

Returns the day of the week of the given date, based on the ISO 8601 standard. Returns `3`, for Wednesday.

```arcade
ISOWeekday(Date(1980, 11, 31))
```


---------------------

## ISOYear

### ISOYear( date ) -> [Number](../../guide/types/#number)

**[Since version 1.12](../../guide/version-matrix)**

Returns the year of the given date based on the ISO 8601 week date calendar.

#### Parameters

- **`date`**: [Date](../../guide/types/#date)  
A date value from which to get the year.

#### Return value: [Number](../../guide/types/#number)

#### Example

Gets the year of the given date, based on the ISO 8601 week date calendar. Returns `1981`, since this date is included in the first week of the following year.

```arcade
ISOYear(Date(1980, 11, 31))
```


---------------------

## Millisecond

### Millisecond( date ) -> [Number](../../guide/types/#number)

Returns the millisecond of the time in the date.

#### Parameters

- **`date`**: [Date](../../guide/types/#date)  
A date value from which to get the millisecond of the time.

#### Return value: [Number](../../guide/types/#number)

#### Example

Gets the millisecond of the current time

```arcade
Millisecond(Now())
```


---------------------

## Minute

### Minute( date ) -> [Number](../../guide/types/#number)

Returns the minute of the time in the given date.

#### Parameters

- **`date`**: [Date](../../guide/types/#date)  
A date value from which to get the minute of the time.

#### Return value: [Number](../../guide/types/#number)

#### Example

Gets the minute of the current time

```arcade
Minute(Now())
```


---------------------

## Month

### Month( date ) -> [Number](../../guide/types/#number)

Returns the month of the given date. Values range from 0-11 where January is `0` and December is `11`.

#### Parameters

- **`date`**: [Date](../../guide/types/#date)  
A date value from which to get the month.

#### Return value: [Number](../../guide/types/#number)

#### Example

Gets the month of the given Date. Returns 11, for the month of December.

```arcade
Month(Date(1980, 11, 31))
```


---------------------

## Now

### Now(  ) -> [Date](../../guide/types/#date)

Returns the current date and time in the local time of the client.

#### Return value: [Date](../../guide/types/#date)

#### Example

Returns the current date and time, e.g. Mon Oct 24 2016 12:09:34 GMT-0700 (PDT)

```arcade
Now()
```


---------------------

## Second

### Second( date ) -> [Number](../../guide/types/#number)

Returns the second of the time in the date.

#### Parameters

- **`date`**: [Date](../../guide/types/#date)  
A date value from which to get the second of the time.

#### Return value: [Number](../../guide/types/#number)

#### Example

Gets the second of the current time

```arcade
Second(Now())
```


---------------------

## Timestamp

### Timestamp(  ) -> [Date](../../guide/types/#date)

**[Since version 1.1](../../guide/version-matrix)**

Returns the current date and time in UTC time.

#### Return value: [Date](../../guide/types/#date)

#### Example

Returns the current date and time in UTC time, e.g. 29 Mar 2017 08:37:33 pm

```arcade
Timestamp()
```


---------------------

## Today

### Today(  ) -> [Date](../../guide/types/#date)

Returns the current date in the local time of the client.

#### Return value: [Date](../../guide/types/#date)

#### Example

Returns the current date with time truncated, e.g. Mon Oct 24 2016 00:00:00 GMT-0700 (PDT)

```arcade
Today()
```


---------------------

## ToLocal

### ToLocal( utcDate ) -> [Date](../../guide/types/#date)

**[Since version 1.1](../../guide/version-matrix)**

Converts the given UTC date to a date value in the local time of the client.

#### Parameters

- **`utcDate`**: [Date](../../guide/types/#date)  
A UTC date value to convert to the local time of the client. This value is assumed to be in UTC time.

#### Return value: [Date](../../guide/types/#date)

#### Example

Convert a UTC date to the local time of the client running the app, e.g. Mon Oct 24 2016 00:00:00 GMT-0700 (PDT)

```arcade
ToLocal(Timestamp())
```


---------------------

## ToUTC

### ToUTC( localDate ) -> [Date](../../guide/types/#date)

**[Since version 1.1](../../guide/version-matrix)**

Converts the given date value from the client's local time to UTC time. Date values in Arcade are already assumed to be UTC. Sometimes dates in databases are stored in local time. Use this function to normalize dates stored in local time with other dates created in Arcade expressions.

#### Parameters

- **`localDate`**: [Date](../../guide/types/#date)  
A date value in local time to convert to UTC time. This value is assumed to be in local time.

#### Return value: [Date](../../guide/types/#date)

#### Example

Returns the current date and time in UTC, e.g. 29 Mar 2017 08:37:33 pm

```arcade
// 29 Mar 2017 01:37:33 pm
Now()
// 29 Mar 2017 08:37:33 pm
ToUTC(Now())
```


---------------------

## Week

### Week( date, startDay? ) -> [Number](../../guide/types/#number)

**[Since version 1.14](../../guide/version-matrix)**

Returns the week number in the year of the given date. Values range from 0-53 where the first week of the year is `0` and the last week of the year is `51`, `52`, or `53`, depending on the year. The first and last weeks may not be a full seven days in length.

#### Parameters

- **`date`**: [Date](../../guide/types/#date)  
A date value from which to get the week.
- **`startDay`** (_Optional_): [Number](../../guide/types/#number)  
A number representing the start day of the week. Sunday = 0; Monday = 1; Tuesday = 2; Wednesday = 3; Thursday = 4; Friday = 5; Saturday = 6. The default is `0` (Sunday).

#### Return value: [Number](../../guide/types/#number)

#### Example

Use the default start of the week (Sunday)

```arcade
Week( Date(1974,0,3) )
// Returns 0
```

Set start of week to Thursday

```arcade
Week( Date(1974,0,3), 4 )
// Returns 1
```

Set start of week to Friday

```arcade
Week( Date(1974,0,3), 5 )
// Returns 0
```

```arcade
Week( Date(1945,8,23) )
// Returns 38
```

```arcade
Week( Date(2022,7,20) )
// Returns 33
```


---------------------

## Weekday

### Weekday( date ) -> [Number](../../guide/types/#number)

Returns the day of the week of the given date. Values range from 0-6 where Sunday is `0` and Saturday is `6`.

#### Parameters

- **`date`**: [Date](../../guide/types/#date)  
A date value from which to return the day of the week.

#### Return value: [Number](../../guide/types/#number)

#### Example

Returns the day of the week of the given date. Returns `3`, for Wednesday.

```arcade
Weekday(Date(1980, 11, 31))
```


---------------------

## Year

### Year( date ) -> [Number](../../guide/types/#number)

Returns the year of the given date.

#### Parameters

- **`date`**: [Date](../../guide/types/#date)  
A date value from which to get the year.

#### Return value: [Number](../../guide/types/#number)

#### Example

Gets the year of the current date

```arcade
Year(Now())
```


---------------------