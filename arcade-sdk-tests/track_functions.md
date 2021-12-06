---
title: Track Functions
description: Documentation for all Track Functions supported in Arcade.
keywords:
  - TrackAccelerationAt
  - TrackAccelerationWindow
  - TrackCurrentAcceleration
  - TrackCurrentDistance
  - TrackCurrentSpeed
  - TrackCurrentTime
  - TrackDistanceAt
  - TrackDistanceWindow
  - TrackDuration
  - TrackFieldWindow
  - TrackGeometryWindow
  - TrackIndex
  - TrackSpeedAt
  - TrackSpeedWindow
  - TrackStartTime
  - TrackWindow
---

# Track Functions

GeoAnalytics Track Expressions are only available when using GeoAnalytics within specific track-enabled tools.

The following functions allow you to create and evaluate expressions with track inputs in GeoAnalytics tools. Tracks are sequentially ordered features with a field specified as a track identifier.

---------------------

[TrackAccelerationAt](#trackaccelerationat) - [TrackAccelerationWindow](#trackaccelerationwindow) - [TrackCurrentAcceleration](#trackcurrentacceleration) - [TrackCurrentDistance](#trackcurrentdistance) - [TrackCurrentSpeed](#trackcurrentspeed) - [TrackCurrentTime](#trackcurrenttime) - [TrackDistanceAt](#trackdistanceat) - [TrackDistanceWindow](#trackdistancewindow) - [TrackDuration](#trackduration) - [TrackFieldWindow](#trackfieldwindow) - [TrackGeometryWindow](#trackgeometrywindow) - [TrackIndex](#trackindex) - [TrackSpeedAt](#trackspeedat) - [TrackSpeedWindow](#trackspeedwindow) - [TrackStartTime](#trackstarttime) - [TrackWindow](#trackwindow)

---------------------

## TrackAccelerationAt

### TrackAccelerationAt( value ) -> [Number](../../guide/types/#number)

**[Since version 1.12](../../guide/version-matrix)**

**Profiles**: [GeoAnalytics](../../guide/profiles/#geoanalytics)

The acceleration at the observation relative to the current observation.

#### Parameter

- **`value`**: [Number](../../guide/types/#number)  
The number of features before or after the current observation.  
The current feature is index 0. Positive values represent features that occur in the future, after the current value. For example, position 1 is the next value in the array. Negative numbers represent features that occurred in the past, before the current feature. For example, -1 is the previous value in the array.

#### Return value: [Number](../../guide/types/#number)

![TrackAccelerationAt_img](../images/track_functions/gax_track_sp_ac_dis_example.png)

#### Examples

Your track has six features, as seen above. The expression returns a number for each feature representing the acceleration value in meters per second squared. In this example, we examine results of feature 1 (p1) with a `value` of 1. The result is equal to the acceleration of feature 2 (p2).

```arcade
var accelerationAt = TrackAccelerationAt(1)
accelerationAt;
// returns 0.0167
```

Your track has six features, as seen above. The expression returns a number for each feature representing the acceleration value in meters per second squared. In this example, we examine results of feature 1 (p1) with a `value` of 3. The result is equal to the acceleration of feature 4 (p4).

```arcade
var accelerationAt = TrackAccelerationAt(3)
accelerationAt;
// returns -0.0014
```


---------------------

## TrackAccelerationWindow

### TrackAccelerationWindow( startIndex, endIndex ) -> [Array](../../guide/types/#array)

**[Since version 1.12](../../guide/version-matrix)**

**Profiles**: [GeoAnalytics](../../guide/profiles/#geoanalytics)

The acceleration values between the first value (inclusive) to the last value (exclusive) in a window around the current observation (0).

#### Parameters

- **`startIndex`**: [Number](../../guide/types/#number)  
The index of the beginning feature. The current feature is index 0. Positive values represent features that occur in the future, after the current value. For example, position 1 is the next value in the array. Negative numbers represent features that occurred in the past, before the current feature. For example, -1 is the previous value in the array.
- **`endIndex`**: [Number](../../guide/types/#number)  
The index of the feature at the end of the window. The current feature is index 0. Positive values represent features that occur in the future, after the current value. For example, position 1 is the next value in the array. Negative numbers represent features that occurred in the past, before the current feature. For example, -1 is the previous value in the array.

#### Return value: [Array](../../guide/types/#array)

![TrackAccelerationWindow_img](../images/track_functions/gax_track_sp_ac_dis_example.png)

#### Examples

Your track has six features, as seen above. The expression returns an array containing the acceleration value for each feature in the specified window. Accelerations are calculated in meters per second squared. In this example, we examine results of feature 3 (p3) when evaluated with a `startIndex` of `-1` and an `endIndex` of `2`.

```arcade
var accelerationWindow = TrackAccelerationWindow(-1, 2)
accelerationWindow;
// returns [0.0167, 0.0056, -0.0014]
```

Your track has six features, as seen above. The expression returns an array containing the acceleration value for each feature in the specified window. Accelerations are calculated in meters per second squared. In this example, we examine results of feature 3 (p3) when evaluated with a `startIndex` of `1` and an `endIndex` of `3`.

```arcade
var accelerationWindow = TrackAccelerationWindow(1, 3)
accelerationWindow;
// returns [-0.0014, 0.0014, -0.0028]
```


---------------------

## TrackCurrentAcceleration

### TrackCurrentAcceleration(  ) -> [Number](../../guide/types/#number)

**[Since version 1.12](../../guide/version-matrix)**

**Profiles**: [GeoAnalytics](../../guide/profiles/#geoanalytics)

The acceleration of the current observation measured between the previous observation and the current observation.

#### Return value: [Number](../../guide/types/#number)

![TrackCurrentAcceleration_img](../images/track_functions/gax_track_sp_ac_dis_example.png)

#### Examples

Your track has six features, as seen above. The expression returns a number for each feature representing the acceleration value in meters per second squared. In the first example, we examine results of feature 2 (p2).

```arcade
var currentAcceleration = TrackCurrentAcceleration()
currentAcceleration;
// returns 0.0167
```

Your track has six features, as seen above. The expression returns a number for each feature representing the acceleration value in meters per second squared. In the following example, we examine results of feature 4 (p4).

```arcade
var currentAcceleration = TrackCurrentAcceleration()
currentAcceleration;
// returns -0.0014
```


---------------------

## TrackCurrentDistance

### TrackCurrentDistance(  ) -> [Number](../../guide/types/#number)

**[Since version 1.12](../../guide/version-matrix)**

**Profiles**: [GeoAnalytics](../../guide/profiles/#geoanalytics)

The sum of the distances travelled between observations from the first to current observation.

#### Return value: [Number](../../guide/types/#number)

![TrackCurrentDistance_img](../images/track_functions/gax_track_sp_ac_dis_example.png)

#### Examples

Your track has six features, as seen above. The expression returns a value for the current feature in the track. In the first example, we examine results for feature 3 (p3). The calculation is `80 + 60 = 140`.

```arcade
var currentDistance = TrackCurrentDistance()
currentDistance;
// returns 140
```

Your track has six features, as seen above. The expression returns a value for the current feature in the track. Your track has six features, as seen above. The expression returns a value for each feature in the track. In the following example, we examine results for feature 6 (p6). The calculation is `25 + 35 + 30 + 80 + 60 = 230`.

```arcade
var currentDistance = TrackCurrentDistance()
currentDistance;
// returns 230
```


---------------------

## TrackCurrentSpeed

### TrackCurrentSpeed(  ) -> [Number](../../guide/types/#number)

**[Since version 1.12](../../guide/version-matrix)**

**Profiles**: [GeoAnalytics](../../guide/profiles/#geoanalytics)

The speed between the previous observation and the current observation.

#### Return value: [Number](../../guide/types/#number)

![TrackCurrentSpeed_img](../images/track_functions/gax_track_sp_ac_dis_example.png)

#### Examples

Your track has six features, as seen above. The expression returns a number for each feature representing the speed calculated in meters per second. In the first example, we examine results of feature 2 (p2). The calculation is `60/60`.

```arcade
var currentSpeed = TrackCurrentSpeed()
currentSpeed;
// returns 1
```

Your track has six features, as seen above. The expression returns a number for each feature representing the speed calculated in meters per second. In the following example, we examine results of feature 6 (p6). The calculation is `25/60`.

```arcade
var currentSpeed = TrackCurrentSpeed()
currentSpeed;
// returns 0.4167
```


---------------------

## TrackCurrentTime

### TrackCurrentTime(  ) -> [Date](../../guide/types/#date)

**[Since version 1.7](../../guide/version-matrix)**

**Profiles**: [GeoAnalytics](../../guide/profiles/#geoanalytics)

Calculates the time on the current feature in a track.

#### Return value: [Date](../../guide/types/#date)

#### Example

Returns the time of the current feature being evaluated. For example, given a track with three features at January 1, 2012, December 9, 2012, and May 3, 2013 the current time will be evaluated for each feature. In this example, it's evaluated at the middle feature, December 9, 2012.

```arcade
TrackCurrentTime();
// returns December 9, 2012
```


---------------------

## TrackDistanceAt

### TrackDistanceAt( index ) -> [Number](../../guide/types/#number)

**[Since version 1.12](../../guide/version-matrix)**

**Profiles**: [GeoAnalytics](../../guide/profiles/#geoanalytics)

The sum of the distances travelled between observations from the first to the current observation plus the given value.

#### Parameter

- **`index`**: [Number](../../guide/types/#number)  
The index of the track feature to calculate distance for. For example, a value of `2` would calculate the distance from the first feature (index `0`) in the track to the third feature (index `2`) in the track.

#### Return value: [Number](../../guide/types/#number)

![TrackDistanceAt_img](../images/track_functions/gax_track_sp_ac_dis_example.png)

#### Examples

Your track has six features, as seen above. The expression returns a value for each feature in the track. In the first example, we examine results when evaluated at feature 2 (p2) with an index value of 2. The calculation is `30 + 80 + 60 = 170`.

```arcade
TrackDistanceAt(2)
// returns 170
```

Your track has six features, as seen above. The expression returns a value for each feature in the track. In the following example, we examine results when evaluated at feature 4 (p4) with an index value of 4. The calculation is `25 + 35 + 30 + 80 + 60 = 230`.

```arcade
TrackDistanceAt(2)
// returns 230
```


---------------------

## TrackDistanceWindow

### TrackDistanceWindow( startIndex, endIndex ) -> [Array](../../guide/types/#array)

**[Since version 1.12](../../guide/version-matrix)**

**Profiles**: [GeoAnalytics](../../guide/profiles/#geoanalytics)

The distances between the first value (inclusive) to the last value (exclusive) in a window about the current observation (0).

#### Parameters

- **`startIndex`**: [Number](../../guide/types/#number)  
The index of the beginning feature. The current feature is index 0. Positive values represent features that occur in the future, after the current value. For example, position 1 is the next value in the array. Negative numbers represent features that occurred in the past, before the current feature. For example, -1 is the previous value in the array.
- **`endIndex`**: [Number](../../guide/types/#number)  
The index of the feature at the end of the window. The current feature is index 0. Positive values represent features that occur in the future, after the current value. For example, position 1 is the next value in the array. Negative numbers represent features that occurred in the past, before the current feature. For example, -1 is the previous value in the array.

#### Return value: [Array](../../guide/types/#array)

![TrackDistanceWindow_img](../images/track_functions/gax_track_sp_ac_dis_example.png)

#### Examples

Your track has six features, as seen above. The expression returns an array containing the distance value for each feature in the window. In the first example, we examine results of feature 3 (p3) when evaluated with a `startIndex` of `-1` and an `endIndex` of `2`.

```arcade
var distanceWindow = TrackDistanceWindow(-1, 2)
distanceWindow;
// returns [60, 140, 170]
```

Your track has six features, as seen above. The expression returns an array containing the distance value for each feature in the window. In the following example, we examine results of feature 5 (p5) when evaluated with a `startIndex` of `-1` and an `endIndex` of `2`.

```arcade
var distanceWindow = TrackDistanceWindow(-1, 2)
distanceWindow;
// returns [170, 205, 230]
```


---------------------

## TrackDuration

### TrackDuration(  ) -> [Number](../../guide/types/#number)

**[Since version 1.7](../../guide/version-matrix)**

**Profiles**: [GeoAnalytics](../../guide/profiles/#geoanalytics)

Calculates the duration of the track from the start feature to the current feature in milliseconds from epoch.

#### Return value: [Number](../../guide/types/#number)

#### Example

Returns the duration of a track that starts on January 1, 2012 until the current feature at May 3, 2013.

```arcade
TrackDuration();
// returns 42163200000
```


---------------------

## TrackFieldWindow

### TrackFieldWindow( fieldName, startIndex, endIndex ) -> [Array](../../guide/types/#array)

**[Since version 1.7](../../guide/version-matrix)**

**Profiles**: [GeoAnalytics](../../guide/profiles/#geoanalytics)

Returns an array of attribute values from the specified `field` for the specified time span. The window function allows you to go forward and backward in time.

#### Parameters

- **`fieldName`**: String  
The field name from which to return values.
- **`startIndex`**: [Number](../../guide/types/#number)  
The index of the beginning feature. The current feature is index `0`. Positive values represent features that occur in the future, after the current value. For example, position `1` is the next value in the array. Negative numbers represent features that occurred in the past, before the current feature. For example, `-1` is the previous value in the array.
- **`endIndex`**: [Number](../../guide/types/#number)  
The index of the feature at the end of the window. The current feature is index `0`. Positive values represent features that occur in the future, after the current value. For example, position `1` is the next value in the array. Negative numbers represent features that occurred in the past, before the current feature. For example, `-1` is the previous value in the array.

#### Return value: [Array](../../guide/types/#array)

#### Examples

Your track has a field with sequentially ordered values of `[10, 20, 30, 40, 50]`. The geometries of the features are `[{x: 1, y: 1},{x: 2, y: 2} ,{x: null, y: null},{x: 4, y: 4}, {x: 5, y: 5}]`. The expression is evaluated at each feature in the track. Results are returned inclusive of the start feature, and exclusive of the end feature. This example is evaluated at the second feature (20) and returns an array of the previous value (-1, inclusive).

```arcade
var window = TrackFieldWindow('MyField', -1,0)
window;
// returns [10]
```

Your track has a field named `Speed` with sequentially ordered values of `[10, 20, 30, 40, 50]`. The geometries of the features are `[{x: 1, y: 1},{x: 2, y: 2} ,{x: null, y: null},{x: 4, y: 4}, {x: 5, y: 5}]`. The expression is evaluated at each feature in the track. For this example, we examine results when evaluated at the third feature (30). Results are returned inclusive of the start feature, and exclusive of the end feature. 

```arcade
var window = TrackFieldWindow('Speed', -2,2)
window;
// returns [10,20,30,40]
```


---------------------

## TrackGeometryWindow

### TrackGeometryWindow( startIndex, endIndex ) -> [Geometry[]](../../guide/types/#geometry)

**[Since version 1.7](../../guide/version-matrix)**

**Profiles**: [GeoAnalytics](../../guide/profiles/#geoanalytics)

Returns an array of geometries for the specified time indices. The window function allows you to go forward and backward in time.

#### Parameters

- **`startIndex`**: [Number](../../guide/types/#number)  
The index of the beginning feature. The current feature is index `0`. Positive values represent features that occur in the future, after the current value. For example, position `1` is the next value in the array. Negative numbers represent features that occurred in the past, before the current feature. For example, `-1` is the previous value in the array.
- **`endIndex`**: [Number](../../guide/types/#number)  
The index of the feature at the end of the window. The current feature is index `0`. Positive values represent features that occur in the future, after the current value. For example, position `1` is the next value in the array. Negative numbers represent features that occurred in the past, before the current feature. For example, `-1` is the previous value in the array.

#### Return value: [Geometry[]](../../guide/types/#geometry)

#### Example

Your track has a field with sequentially ordered values of `[10, 20, 30, 40, 50]`. The geometries of the features are `[{x: 1, y: 1},{x: 2, y: 2} ,{x: null, y: null},{x: 4, y: 4}, {x: 5, y: 5}]`. The expression is evaluated at each feature in the track. For this example, we examine results when evaluated at the third feature (30). Results are returned inclusive of the start feature, and exclusive of the end feature

```arcade
var window = TrackGeometryWindow(-2,2)
window;
// returns [{x: 1, y: 1},{x: 2, y: 2} ,{x: null, y: null},{x: 4, y: 4}]
```


---------------------

## TrackIndex

### TrackIndex(  ) -> [Number](../../guide/types/#number)

**[Since version 1.7](../../guide/version-matrix)**

**Profiles**: [GeoAnalytics](../../guide/profiles/#geoanalytics)

Returns the index of the feature being calculated. Features are indexed in order of time within a track.

#### Return value: [Number](../../guide/types/#number)

#### Example

Returns the index of the first feature in a track.

```arcade
TrackIndex() // returns 0
```


---------------------

## TrackSpeedAt

### TrackSpeedAt( value ) -> [Number](../../guide/types/#number)

**[Since version 1.12](../../guide/version-matrix)**

**Profiles**: [GeoAnalytics](../../guide/profiles/#geoanalytics)

The speed at the observation relative to the current observation. For example, at value 2, it's the speed at the observation two observations after the current.

#### Parameter

- **`value`**: [Number](../../guide/types/#number)  
The number of features before or after the current observation. The current feature is index 0. Positive values represent features that occur in the future, after the current value. For example, position 1 is the next value in the array. Negative numbers represent features that occurred in the past, before the current feature. For example, -1 is the previous value in the array.

#### Return value: [Number](../../guide/types/#number)

![TrackSpeedAt_img](../images/track_functions/gax_track_sp_ac_dis_example.png)

#### Examples

Your track has six features, as seen above. The expression returns a number for each feature representing the speed calculated in meters per second. In the first example, we examine results of feature 1 (p1) with a `value` of 2. The calculation is `80/60`.

```arcade
var speedAt = TrackSpeedAt(2)
speedAt;
// returns 1.33
```

Your track has six features, as seen above. The expression returns a number for each feature representing the speed calculated in meters per second. In the following example, we examine results of feature 3 (p3) with a `value` of -1. The calculation is `60/60`.

```arcade
var speedAt = TrackSpeedAt(2)
speedAt;
// returns 1
```


---------------------

## TrackSpeedWindow

### TrackSpeedWindow( startIndex, endIndex ) -> [Array](../../guide/types/#array)

**[Since version 1.12](../../guide/version-matrix)**

**Profiles**: [GeoAnalytics](../../guide/profiles/#geoanalytics)

The speed values between the first value (inclusive) to the last value (exclusive) in a window around the current observation (0).

#### Parameters

- **`startIndex`**: [Number](../../guide/types/#number)  
The index of the beginning feature. The current feature is index 0. Positive values represent features that occur in the future, after the current value. For example, position 1 is the next value in the array. Negative numbers represent features that occurred in the past, before the current feature. For example, -1 is the previous value in the array.
- **`endIndex`**: [Number](../../guide/types/#number)  
The index of the feature at the end of the window. The current feature is index 0. Positive values represent features that occur in the future, after the current value. For example, position 1 is the next value in the array. Negative numbers represent features that occurred in the past, before the current feature. For example, -1 is the previous value in the array.

#### Return value: [Array](../../guide/types/#array)

![TrackSpeedWindow_img](../images/track_functions/gax_track_sp_ac_dis_example.png)

#### Examples

Your track has six features, as seen above. The expression returns an array containing the speed value for each feature in the specified window. Speeds are calculated in meters per second. In this example, we examine results of feature 3 (p3) when evaluated with a `startIndex` of `-1` and an `endIndex` of `2`.

```arcade
var speedWindow = TrackSpeedWindow(-1, 2)
speedWindow // returns [1, 1.3, 0.5]
```

Your track has six features, as seen above. The expression returns an array containing the speed value for each feature in the specified window. Speeds are calculated in meters per second. In this example, we examine results of feature 3 (p3) when evaluated with a `startIndex` of `1` and an `endIndex` of `3`.

```arcade
var speedWindow = TrackSpeedWindow(1,3)
speedWindow // returns [0.5, 0.583, 0.4167]
```


---------------------

## TrackStartTime

### TrackStartTime(  ) -> [Date](../../guide/types/#date)

**[Since version 1.7](../../guide/version-matrix)**

**Profiles**: [GeoAnalytics](../../guide/profiles/#geoanalytics)

Calculates the start time of a track.

#### Return value: [Date](../../guide/types/#date)

#### Example

Returns the start time of a track that spans from January 1, 2012 to May 3, 2013.

```arcade
TrackStartTime() // returns January 1, 2012
```


---------------------

## TrackWindow

### TrackWindow( startIndex, endIndex ) -> [Feature[]](../../guide/types/#feature)

**[Since version 1.7](../../guide/version-matrix)**

**Profiles**: [GeoAnalytics](../../guide/profiles/#geoanalytics)

Returns an array of features for the specified time index. This function allows you to go forward and backward in time.

#### Parameters

- **`startIndex`**: [Number](../../guide/types/#number)  
The index of the beginning feature. The current feature is index `0`. Positive values represent features that occur in the future, after the current value. For example, position `1` is the next value in the array. Negative numbers represent features that occurred in the past, before the current feature. For example, `-1` is the previous value in the array.
- **`endIndex`**: [Number](../../guide/types/#number)  
The index of the feature at the end of the window. The current feature is index `0`. Positive values represent features that occur in the future, after the current value. For example, position `1` is the next value in the array. Negative numbers represent features that occurred in the past, before the current feature. For example, `-1` is the previous value in the array.

#### Return value: [Feature[]](../../guide/types/#feature)

#### Examples

Your track has a field with sequentially ordered values of `[10, 20, 30, 40, 50]`. The geometries of the features are `[{x: 1, y: 1},{x: 2, y: 2} ,{x: null, y: null},{x: 4, y: 4}, {x: 5, y: 5}]`. The expression is evaluated at each feature in the track. Results are returned inclusive of the start feature, and exclusive of the end feature. This example is evaluated at the second feature (20) and returns an array of a single value -- the previous feature.

```arcade
var window = TrackWindow(-1,0)
window;
// returns [{'geometry': {x: 1, y: 1}}, {'attributes': {'MyField' : 10, 'trackName':'ExampleTrack1'}}]
```

Your track has a field with sequentially ordered values of `[10, 20, 30, 40, 50]`. The geometries of the features are `[{x: 1, y: 1},{x: 2, y: 2} ,{x: null, y: null},{x: 4, y: 4}, {x: 5, y: 5}]`. The expression is evaluated at each feature in the track. For this example, we examine results when evaluated at the third feature (30). Results are returned inclusive of the start feature, and exclusive of the end feature.

```arcade
var window = TrackWindow(-2,2)
window;
/* returns
[{
  geometry: [{
    x: 1,
    y: 1
  }, {
    x: 2,
    y: 2
  }, {
    x: null,
     y: null
  }, {
    x: 4,
    y: 4
  }]
}, {
  attributes: [{
    MyField: 10,
    trackName: 'ExampleTrack1'
  }, {
    MyField: 20,
    trackName: 'ExampleTrack1'
  }, {
    MyField: 30,
    trackName: 'ExampleTrack1'
  }, {
    MyField: 40,
    trackName: 'ExampleTrack1'
  }]
}]
```


---------------------