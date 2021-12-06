---
title: Geometry Functions
description: Documentation for all Geometry Functions supported in Arcade.
keywords:
  - Angle
  - Area
  - AreaGeodetic
  - Bearing
  - Buffer
  - BufferGeodetic
  - Centroid
  - Clip
  - Contains
  - ConvertDirection
  - Crosses
  - Cut
  - Densify
  - DensifyGeodetic
  - Difference
  - Disjoint
  - Distance
  - DistanceGeodetic
  - EnvelopeIntersects
  - Equals
  - Extent
  - Generalize
  - Geometry
  - Intersection
  - Intersects
  - IsSelfIntersecting
  - IsSimple
  - Length
  - Length3D
  - LengthGeodetic
  - MultiPartToSinglePart
  - Multipoint
  - Offset
  - Overlaps
  - Point
  - Polygon
  - Polyline
  - Relate
  - RingIsClockwise
  - Rotate
  - SetGeometry
  - Simplify
  - SymmetricDifference
  - Touches
  - Union
  - Within
---

# Geometry Functions

The following functions allow you to create and evaluate geometry objects. Please note that if your input has more than one geometry, they must have the same spatial reference.

Since Arcade expressions execute for each feature, using multiple geometry operations within the context of the labeling and visualization profiles can be expensive and severely impact the performance of the application. Also note that geometries fetched from feature services, especially polylines and polygons, are generalized according to the view's scale resolution. Be aware that using a feature's geometry (i.e. `$feature`) as input to any geometry function will yield results only as precise as the view scale. Therefore, results returned from geometry operations in the visualization and labeling profiles may be different at each scale level. Use these functions at your discretion within these contexts.

Geometry functions are not supported in the [Dashboard formatting profile](../../guide/profiles/#dashboard-formatting).

### Units reference

If a function references units, then any of the values described in the table below may be used. Units can either be identified as a number or a string. If the value is a number, it will be based on the standard [referenced here](https://developers.arcgis.com/java/10-2/api-reference/constant-values.html#com.esri.core.geometry.AreaUnit.Code.ACRE). Where appropriate, linear and areal units may be used interchangeably. For example, if calculating an area and `meters` is specified as the unit, then the unit will be treated as `square-meters` and vice versa.

| Unit value | Alternate values |
| :--- | :--- |
| `acres`* | `acre`, `ac` |
| `feet` | `foot`, `ft`, `square-feet`, `square-foot`, `squarefeet`, `squarefoot` |
| `hectares`* | `hectare`, `ha` |
| `kilometers` | `kilometer`, `km`, `square-kilometers`, `square-kilometer`, `squarekilometers`, `squarekilometer` |
| `miles` | `mile`, `square-miles`, `square-mile`, `squaremiles`, `squaremile` |
| `nautical-miles` | `nautical-mile`, `square-nautical-miles`, `square-nautical-mile`, `squarenauticalmiles`, `squarenauticalmile` |
| `meters` | `meter`, `m`, `square-meters`, `square-meter`, `squaremeters`, `squaremeter` |
| `yards` | `yard`, `yd`, `square-yards`, `square-yard`, `squareyards`, `squareyard` |


\* Indicates the unit may only be used for calculating areas.

---------------------

## Angle

This function has 2 signatures:

- [Angle( pointA, pointB ) -> Number](#angle1)
- [Angle( pointA, pointB, pointC ) -> Number](#angle2)

<a name="angle1"></a>
### Angle( pointA, pointB ) -> [Number](../../guide/types/#number)

**[Since version 1.7](../../guide/version-matrix)**

Returns the arithmetic angle of a line between two points in degrees (0 - 360). The angle is measured in a counter-clockwise direction relative to east. For example, an angle of 90 degrees points due north.

Only the x-y plane is considered for the measurement. Any z-coordinates are ignored. Point features can be used instead of any or both Point geometries. _If the points are identical, then an angle of 0 degrees is returned._

See [bearing](../../function-reference/geometry_functions/#bearing).

#### Parameters

- **`pointA`**: [Point](../../guide/types/#point) \| [Feature](../../guide/types/#feature)  
The first Point or Feature used to calculate the angle.
- **`pointB`**: [Point](../../guide/types/#point) \| [Feature](../../guide/types/#feature)  
The second Point or Feature used to calculate the angle.

#### Return value: [Number](../../guide/types/#number)

![Angle_img](../images/geometry_functions/angle-ab.jpg)

#### Example

Returns the angle from a Point to a Feature, in degrees

```arcade
var pointA = Point({ "x":976259, "y":8066511, "spatialReference": { "wkid": 3857 } });
Angle(pointA, $feature)
```


<a name="angle2"></a>
### Angle( pointA, pointB, pointC ) -> [Number](../../guide/types/#number)

**[Since version 1.7](../../guide/version-matrix)**

Returns the arithmetic angle of a line between three points in degrees (0 - 360). The angle is measured around `pointB` in a counter-clockwise direction, from `pointA` to `pointC`.

Only the x-y plane is considered for the measurement. Any z-coordinates are ignored. Point features can be used instead of either or all Point geometries. _If the points are identical, then an angle of 0 or 180 degrees is returned (depending internal arithmetic)._

See [bearing](../../function-reference/geometry_functions/#bearing).

#### Parameters

- **`pointA`**: [Point](../../guide/types/#point) \| [Feature](../../guide/types/#feature)  
The first Point or Feature used to calculate the angle.
- **`pointB`**: [Point](../../guide/types/#point) \| [Feature](../../guide/types/#feature)  
The second Point or Feature used to calculate the angle.
- **`pointC`**: [Point](../../guide/types/#point) \| [Feature](../../guide/types/#feature)  
The third Point or Feature used to calculate the angle.

#### Return value: [Number](../../guide/types/#number)

![Angle_img](../images/geometry_functions/angle-abc.jpg)

#### Example

Returns the angle between two points around the feature, in degrees

```arcade
var pointA = Point({ "x":976259, "y":8066511, "spatialReference": { "wkid": 3857 } });
var pointC = Point({ "x":308654, "y":9005421, "spatialReference": { "wkid": 3857 } });
Angle(pointA, $feature, pointC)
```


---------------------

## Area

This function has 2 signatures:

- [Area( polygon, unit? ) -> Number](#area1)
- [Area( features, unit? ) -> Number](#area2)

<a name="area1"></a>
### Area( polygon, unit? ) -> [Number](../../guide/types/#number)

**[Since version 1.7](../../guide/version-matrix)**

Returns the area of the input geometry or Feature in the given units. This is a planar measurement using Cartesian mathematics.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`polygon`**: [Polygon](../../guide/types/#polygon) \| [Feature](../../guide/types/#feature) \| Points[]  
The Polygon or Feature for which to calculate the planar area.
- **`unit`** (_Optional_): [Text](../../guide/types/#text) \| [Number](../../guide/types/#number)  
Measurement unit of the return value. Use one of the string values listed in the [Units reference](https://developers.arcgis.com/arcade/function-reference/geometry_functions/#units-reference).

#### Return value: [Number](../../guide/types/#number)

#### Example

Returns the area of the feature in square meters

```arcade
Area($feature, 'square-meters')
```


<a name="area2"></a>
### Area( features, unit? ) -> [Number](../../guide/types/#number)

**[Since version 1.7](../../guide/version-matrix)**

Returns the area of the input FeatureSet in the given units. This is a planar measurement using Cartesian mathematics.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
The FeatureSet for which to calculate the planar area.
- **`unit`** (_Optional_): [Text](../../guide/types/#text) \| [Number](../../guide/types/#number)  
Measurement unit of the return value. Use one of the string values listed in the [Units reference](https://developers.arcgis.com/arcade/function-reference/geometry_functions/#units-reference).

#### Return value: [Number](../../guide/types/#number)

#### Example

Returns the area of the layer in square kilometers

```arcade
Area($layer, 'square-kilometers')
```


---------------------

## AreaGeodetic

This function has 2 signatures:

- [AreaGeodetic( polygon, unit? ) -> Number](#areageodetic1)
- [AreaGeodetic( features, unit? ) -> Number](#areageodetic2)

<a name="areageodetic1"></a>
### AreaGeodetic( polygon, unit? ) -> [Number](../../guide/types/#number)

**[Since version 1.7](../../guide/version-matrix)**

Returns the geodetic area of the input geometry or Feature in the given units. This is more reliable measurement of area than [Area()](../../function-reference/geometry_functions/#area) because it takes into account the Earth's curvature. Support is limited to geometries with a Web Mercator (wkid 3857) or a WGS 84 (wkid 4326) spatial reference.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](https://developers.arcgis.com/arcade/function-reference/geometry_functions/).

#### Parameters

- **`polygon`**: [Polygon](../../guide/types/#polygon) \| [Feature](../../guide/types/#feature) \| Points[]  
The Polygon or Feature for which to calculate the geodetic area.
- **`unit`** (_Optional_): [Text](../../guide/types/#text) \| [Number](../../guide/types/#number)  
Measurement unit of the return value. Use one of the string values listed in the [Units reference](https://developers.arcgis.com/arcade/function-reference/geometry_functions/#units-reference).

#### Return value: [Number](../../guide/types/#number)

#### Example

Returns the geodetic area of the feature in square meters

```arcade
AreaGeodetic($feature, 'square-meters')
```


<a name="areageodetic2"></a>
### AreaGeodetic( features, unit? ) -> [Number](../../guide/types/#number)

**[Since version 1.7](../../guide/version-matrix)**

Returns the geodetic area of the input FeatureSet in the given units. This is more reliable measurement of area than [Area()](../../function-reference/geometry_functions/#area) because it takes into account the Earth's curvature. Support is limited to geometries with a Web Mercator (wkid 3857) or a WGS 84 (wkid 4326) spatial reference.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](https://developers.arcgis.com/arcade/function-reference/geometry_functions/).

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
The FeatureSet for which to calculate the geodetic area.
- **`unit`** (_Optional_): [Text](../../guide/types/#text) \| [Number](../../guide/types/#number)  
Measurement unit of the return value. Use one of the string values listed in the [Units reference](https://developers.arcgis.com/arcade/function-reference/geometry_functions/#units-reference).

#### Return value: [Number](../../guide/types/#number)

#### Example

Returns the geodetic area of the layer in square kilometers

```arcade
AreaGeodetic($layer, 'square-kilometers')
```


---------------------

## Bearing

This function has 2 signatures:

- [Bearing( pointA, pointB ) -> Number](#bearing1)
- [Bearing( pointA, pointB, pointC ) -> Number](#bearing2)

<a name="bearing1"></a>
### Bearing( pointA, pointB ) -> [Number](../../guide/types/#number)

**[Since version 1.7](../../guide/version-matrix)**

Returns the geographic angle of a line between two points in degrees (0 - 360). The bearing is measured in a clockwise direction relative to north. For example, a bearing of 225 degrees represents a southwest orientation.

Only the x-y plane is considered for the measurement. Any z-coordinates are ignored. Point features can be used instead of either or both Point geometries. _If the points are identical, then an angle of 0 is returned._

See also [angle](../../function-reference/geometry_functions/#angle).

#### Parameters

- **`pointA`**: [Point](../../guide/types/#point) \| [Feature](../../guide/types/#feature)  
The first point used to calculate the bearing.
- **`pointB`**: [Point](../../guide/types/#point) \| [Feature](../../guide/types/#feature)  
The second point used to calculate the bearing.

#### Return value: [Number](../../guide/types/#number)

![Bearing_img](../images/geometry_functions/bearing-ab.jpg)

#### Example

Returns the bearing from a point to the feature, in degrees

```arcade
var pointA = Point({ "x":976259, "y":8066511, "spatialReference": { "wkid": 3857 } });
Bearing(pointA,$feature)
```


<a name="bearing2"></a>
### Bearing( pointA, pointB, pointC ) -> [Number](../../guide/types/#number)

**[Since version 1.7](../../guide/version-matrix)**

Returns the geographic angle of a line between three points in degrees (0 - 360). The bearing is measured around `pointB` in a clockwise direction, from `pointA` to `pointC`.

Only the x-y plane is considered for the measurement. Any z-coordinates are ignored. Point features can be used instead of any or all Point geometries. _If the points are identical, then an angle of 0 or 180 degrees is returned (depending internal arithmetic)._

See also [angle](../../function-reference/geometry_functions/#angle).

#### Parameters

- **`pointA`**: [Point](../../guide/types/#point) \| [Feature](../../guide/types/#feature)  
The first point used to calculate the bearing.
- **`pointB`**: [Point](../../guide/types/#point) \| [Feature](../../guide/types/#feature)  
The second point used to calculate the bearing.
- **`pointC`**: [Point](../../guide/types/#point) \| [Feature](../../guide/types/#feature)  
The third point used to calculate the bearing.

#### Return value: [Number](../../guide/types/#number)

![Bearing_img](../images/geometry_functions/bearing-abc.jpg)

#### Example

Returns the bearing between two points around the feature, in degrees

```arcade
var pointA = Point({ "x":976259, "y":8066511, "spatialReference": { "wkid": 3857 } });
var pointC = Point({ "x":308654, "y":9005421, "spatialReference": { "wkid": 3857 } });
Bearing(pointA,$feature,pointC)
```


---------------------

## Buffer

### Buffer( geometry, distance, unit? ) -> [Polygon](../../guide/types/#polygon)

**[Since version 1.3](../../guide/version-matrix)**

Returns the planar (or Euclidean) buffer at a specified distance around the input geometry. This is a planar measurement using Cartesian mathematics.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`geometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The geometry to buffer.
- **`distance`**: [Number](../../guide/types/#number)  
The distance to buffer from the geometry.
- **`unit`** (_Optional_): [Text](../../guide/types/#text) \| [Number](../../guide/types/#number)  
Measurement unit of the buffer `distance`. Use one of the string values listed in the [Units reference](https://developers.arcgis.com/arcade/function-reference/geometry_functions/#units-reference).

#### Return value: [Polygon](../../guide/types/#polygon)

![Buffer_img](../images/geometry_functions/buffer.jpg)

#### Example

Returns a polygon representing a 1/2-mile buffer around the input geometry

```arcade
Buffer($feature, 0.5, 'miles')
```


---------------------

## BufferGeodetic

### BufferGeodetic( geometry, distance, unit? ) -> [Polygon](../../guide/types/#polygon)

**[Since version 1.3](../../guide/version-matrix)**

Returns the geodetic buffer at a specified distance around the input geometry. This is a geodesic measurement, which calculates distances on an ellipsoid. Support is limited to geometries with a Web Mercator (wkid 3857) or a WGS 84 (wkid 4326) spatial reference.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`geometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The geometry to buffer.
- **`distance`**: [Number](../../guide/types/#number)  
The distance to buffer from the geometry.
- **`unit`** (_Optional_): [Text](../../guide/types/#text) \| [Number](../../guide/types/#number)  
Measurement unit of the buffer `distance`. Use one of the string values listed in the [Units reference](https://developers.arcgis.com/arcade/function-reference/geometry_functions/#units-reference).

#### Return value: [Polygon](../../guide/types/#polygon)

#### Example

Returns a polygon representing a 1/2-mile buffer around the input geometry

```arcade
BufferGeodetic($feature, 0.5, 'miles')
```


---------------------

## Centroid

### Centroid( polygon ) -> [Point](../../guide/types/#point)

**[Since version 1.7](../../guide/version-matrix)**

Returns the centroid of the input geometry.

#### Parameter

- **`polygon`**: [Polygon](../../guide/types/#polygon) \| [Feature](../../guide/types/#feature) \| [Point[]](../../guide/types/#point)  
The polygon or array of points composing a polygon.

#### Return value: [Point](../../guide/types/#point)

#### Examples

Returns the centroid of the given polygon

```arcade
Centroid($feature)
```

Returns the centroid of the given polygon ring

```arcade
var ringPoints = Geometry($feature).rings[0];
Centroid(ringPoints);
```


---------------------

## Clip

### Clip( geometry, envelope ) -> [Geometry](../../guide/types/#geometry)

**[Since version 1.3](../../guide/version-matrix)**

Calculates the clipped geometry from a target geometry by an envelope.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`geometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The geometry to be clipped.
- **`envelope`**: [Extent](../../guide/types/#extent)  
The envelope used to clip the `geometry`.

#### Return value: [Geometry](../../guide/types/#geometry)

![Clip_img](../images/geometry_functions/clip.jpg)

#### Example

Returns the area of the clipped geometry

```arcade
var envelope = Extent({ ... });
Area(Clip($feature, envelope), 'square-miles');
```


---------------------

## Contains

This function has 2 signatures:

- [Contains( containerGeometry, insideGeometry ) -> Boolean](#contains1)
- [Contains( containerGeometry, insideFeatures ) -> FeatureSet](#contains2)

<a name="contains1"></a>
### Contains( containerGeometry, insideGeometry ) -> [Boolean](../../guide/types/#boolean)

**[Since version 1.7](../../guide/version-matrix)**

Indicates if one geometry contains another geometry. In the graphic below, the red highlight indicates the scenarios where the function will return `true`.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`containerGeometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The geometry that is tested for the 'contains' relationship to `insideGeometry`. Think of this geometry as the potential 'container' of the `insideGeometry`.
- **`insideGeometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The geometry that is tested for the 'within' relationship to the `containerGeometry`.

#### Return value: [Boolean](../../guide/types/#boolean)

![Contains_img](../images/geometry_functions/contains.jpg)

#### Example

Returns true if the feature is contained within the given polygon

```arcade
var container = Polygon({ ... });
Contains(containerGeometry, $feature);
```


<a name="contains2"></a>
### Contains( containerGeometry, insideFeatures ) -> [FeatureSet](../../guide/types/#featureset)

**[Since version 1.7](../../guide/version-matrix)**

Returns features from a FeatureSet that are contained within the input geometry. In the graphic below, the red highlight illustrates the spatial relationships where the function will return features.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`containerGeometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The geometry that is tested for the 'contains' relationship to `insideFeatures`. Think of this geometry as the potential 'container' of the `insideFeatures`.
- **`insideFeatures`**: [FeatureSet](../../guide/types/#featureset)  
The FeatureSet that is tested for the 'within' relationship to the `containerGeometry`.

#### Return value: [FeatureSet](../../guide/types/#featureset)

![Contains_img](../images/geometry_functions/contains.jpg)

#### Example

Returns the number of features that are within the given polygon

```arcade
var parcels = FeatureSetByName($map, 'parcels')
var projectArea = $feature;
Count(Contains(projectArea, parcels));
```


---------------------

## ConvertDirection

### ConvertDirection( input, inputSpec, outputSpec ) -> [Array](../../guide/types/#array) \| [Number](../../guide/types/#number) \| [Text](../../guide/types/#text)

**[Since version 1.13](../../guide/version-matrix)**

Angles can have several interpretations and can be represented as a number, a text, or a well formed array. This function takes one input representation and converts it to another.

The input value is described by a dictionary that specified the type of angle and the type of direction. Examples:

| input | angle type | direction type |
| :--- | :--- | :--- |
| 12.34 | dms, degrees, radians, gradians | north, south, polar |
| 12.3456 | dms, degrees, radians, gradians | north, south, polar |
| [12,34,56] | dms | north, south, polar |
| ['N',12.34,'W'] | dms, degrees, radians, gradians | quadrant |
| ['N',12,34,56,'W'] | dms | quadrant |
| '12.34' | dms, degrees, radians, gradians | north, south, polar |
| '12 34 56' | dms | north, south, polar |
| 'N 12.34 W' | dms, degrees, radians, gradians | quadrant |
| 'N 12 34 56 W' | dms | quadrant |


If the `angleType` and `directionType` are not appropriate for the input, then the conversion will fail.

The desired output value is as well described by a dictionary that specidies output type, angle type, direction type, and an optional format for text ouput.

If the output type is `value`:  
 - an array will be returned for angle type `dms` or for direction type `quadrant`  
 - a number will be returned for all the other cases

If the output type is `text`, then default padding and delimeters will be used unless the optional`format` property is provided.  
`format` controls order, spacing, padding, and delimeters in the output text.  
Strings of format specifier characters before a decimal point indicate minimum padding (e.g. `DDD -> 000`).  
Strings of format characters after a decimal point indicate precision (e.g. `D.DD -> 0.00`).

Supported `format` characters:

| Code | Meaning |
| :--- | :--- |
| `D` | Decimal Degrees |
| `R` | Radians |
| `G` | Gradians |
| `d` | DMS Degrees |
| `m` | DMS Minutes |
| `s` | DMS Seconds |
| `P` | Long Meridian (e.g. `North` vs. `South`) |
| `p` | Short Meridian (e.g. `N` vs. `S`) |
| `B` | Long direction (e.g. `East` vs. `West`) |
| `b` | Short direction (e.g. `E` vs. `W`) |
| `[ ]` | Escape characters |


For `dms` formatting, if the `s` is not used then `m` will round to the nearest minute. Similarly, if `m` is not used then `d` will round.

#### Parameters

- **`input`**: [Array](../../guide/types/#array) \| [Number](../../guide/types/#number) \| [Text](../../guide/types/#text)  
A raw representation of the bearing. The type of `input` and the values of the `inputSpec` dictate how the input is parsed.
- **`inputSpec`**: [Dictionary](../../guide/types/#dictionary)  
Contains information about how to interpret input.

  - **`angleType`**: [Text](../../guide/types/#text)  
Describes the input angle unit.  
Supported Values: `DEGREES`, `DMS`, `RADIANS`, `GONS`, `GRADIANS`
  - **`directionType`**: [Text](../../guide/types/#text)  
Describes the input bearing's meridian and direction.  
Supported Values: `NORTH`, `SOUTH`, `POLAR`, `QUADRANT`
- **`outputSpec`**: [Dictionary](../../guide/types/#dictionary)  
Contains information about how to format the output. [See the properties of the outputSpec here.](https://developers.arcgis.com/arcade/function-reference/geometry_functions/#outputspec)

  - **`outputType`**: [Text](../../guide/types/#text)  
Controls output type.  
Supported Values: `value`, `text`
  - **`angleType`**: [Text](../../guide/types/#text)  
Describes the output angle unit.  
Supported Values: `DEGREES`, `DMS`, `RADIANS`, `GONS`, `GRADIANS`
  - **`directionType`**: [Text](../../guide/types/#text)  
Describes the output bearing's meridian and direction.  
Supported Values: `NORTH`, `SOUTH`, `POLAR`, `QUADRANT`
  - **`format`** (_Optional_): [Text](../../guide/types/#text)  
Controls text formatting. Only applicable if `outputType` is `text`.

#### Return value: [Array](../../guide/types/#array) \| [Number](../../guide/types/#number) \| [Text](../../guide/types/#text)

#### Examples

Examples where the `outputType` is `value`.

```arcade
ConvertDirection( 30, {directionType:'North', angleType: 'Degrees'}, {directionType:'Quadrant', angleType: 'DMS', outputType: 'value'})
// returns ['N', 30, 0, 0, 'E']
 
ConvertDirection( 25.99, {directionType:'North', angleType : 'Gradians'}, {directionType:'North', outputType: 'value', angleType : 'Gradians'})
// returns 25.99
 
ConvertDirection( 1, {directionType:'North', angleType: 'DEGREES'}, {directionType: 'Quadrant', angleType: 'Degrees', outputType: 'value'})
// returns ['N',1,'E']
 
ConvertDirection( 0.9, {directionType: 'North', angleType: 'degrees'}, {directionType:'North', angleType: 'gradians', outputType: 'value'})
// returns 1.0 
 
ConvertDirection( 180.0, {directionType:'North', angleType: 'degrees'}, {directionType:'North', angleType: 'radians', outputType : 'value'})
// returns PI
```

Examples where `outputType` is `text`.

```arcade
ConvertDirection( 25.34, {directionType: 'North', angleType: 'DEGREES'}, {directionType:'North', outputType: 'text', format: 'DDDD.D'})
// returns '0025.3'
 
ConvertDirection( 25.34, {directionType: 'North', angleType: 'DEGREES'}, {directionType:'North', outputType: 'text', format: 'R'})
// returns '0'
 
ConvertDirection( 25.34, {directionType: 'North', angleType: 'DEGREES'}, {directionType:'North', outputType: 'text', format: '[DD.DD]'})
// returns 'DD.DD'
 
ConvertDirection( 25.34, {directionType:'North', angleType: 'DEGREES'}, {directionType:'quadrant', outputType: 'text', format: 'P B'})
// returns 'North East'
 
ConvertDirection( [001,01,59.99], {directionType:'North', angleType: 'DMS'}, {directionType:'North', angleType: 'DMS', outputType: 'text', format: 'dddA mm[B] ssC'})
// returns '001A 02B 00C'
```


---------------------

## Crosses

This function has 2 signatures:

- [Crosses( geometry1, geometry2 ) -> Boolean](#crosses1)
- [Crosses( features, crossingGeometry ) -> FeatureSet](#crosses2)

<a name="crosses1"></a>
### Crosses( geometry1, geometry2 ) -> [Boolean](../../guide/types/#boolean)

**[Since version 1.3](../../guide/version-matrix)**

Indicates if one geometry crosses another geometry. In the graphic below, the red highlight indicates the scenarios where the function will return `true`.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`geometry1`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The geometry to cross.
- **`geometry2`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The geometry being crossed.

#### Return value: [Boolean](../../guide/types/#boolean)

![Crosses_img](../images/geometry_functions/crosses.jpg)

#### Example

Returns true if the feature crosses the given polygon

```arcade
var geom2 = Polygon({ ... });
Crosses($feature, geom2);
```


<a name="crosses2"></a>
### Crosses( features, crossingGeometry ) -> [FeatureSet](../../guide/types/#featureset)

**[Since version 1.3](../../guide/version-matrix)**

Returns features from a FeatureSet that cross the input geometry. In the graphic below, the red highlight illustrates the spatial relationships where the function will return features.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
The features to test the crosses relationship with the input `crossingGeometry`.
- **`crossingGeometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The geometry being crossed.

#### Return value: [FeatureSet](../../guide/types/#featureset)

![Crosses_img](../images/geometry_functions/crosses.jpg)

#### Example

Returns the number of features in the FeatureSet that cross the given polygon

```arcade
var geom2 = Polygon({ ... });
Count( Crosses($layer, geom2) );
```


---------------------

## Cut

### Cut( polylineOrPolygon, cutter ) -> [Geometry[]](../../guide/types/#geometry)

**[Since version 1.3](../../guide/version-matrix)**

Splits the input Polyline or Polygon where it crosses a cutting Polyline. For Polylines, all resulting left cuts are grouped together in the first Geometry. Right cuts and coincident cuts are grouped in the second Geometry. Each undefined cut, along with any uncut parts, are output as separate Polylines.

For Polygons, all resulting left cuts are grouped in the first Polygon, all right cuts are grouped in the second Polygon, and each undefined cut, along with any left-over parts after cutting, are output as a separate Polygon. If no cuts are returned then the array will be empty. An undefined cut will only be produced if a left cut or right cut was produced and there was a part left over after cutting, or a cut is bounded to the left and right of the cutter.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`polylineOrPolygon`**: [Polyline](../../guide/types/#polyline) \| [Polygon](../../guide/types/#polygon) \| [Feature](../../guide/types/#feature)  
The geometry to cut.
- **`cutter`**: [Polyline](../../guide/types/#polyline) \| [Feature](../../guide/types/#feature)  
The Polyline used to cut the `geometry`.

#### Return value: [Geometry[]](../../guide/types/#geometry)

![Cut_img](../images/geometry_functions/cut.jpg)

#### Example

Cuts the feature's geometry with the given polyline

```arcade
var cutter = Polyline({ ... });
Cut($feature, cutter));
```


---------------------

## Densify

### Densify( geometry, maxSegmentLength, unit? ) -> [Geometry](../../guide/types/#geometry)

**[Since version 1.11](../../guide/version-matrix)**

Densifies geometries by inserting vertices to create segments no longer than the specified interval.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`geometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The input geometry to be densified.
- **`maxSegmentLength`**: [Number](../../guide/types/#number)  
The maximum segment length allowed. Must be a positive value.
- **`unit`** (_Optional_): [Text](../../guide/types/#text) \| [Number](../../guide/types/#number)  
Measurement unit for maxSegmentLength. Defaults to the units of the input geometry. Use one of the string values listed in the [Units reference](https://developers.arcgis.com/arcade/function-reference/geometry_functions/#units-reference).

#### Return value: [Geometry](../../guide/types/#geometry)

![Densify_img](../images/geometry_functions/densify.jpg)

#### Example

Returns the densified geometry with a maximum segment length of 10 m

```arcade
var maxLength = 10;
Densify($feature, maxLength, 'meters');
```


---------------------

## DensifyGeodetic

### DensifyGeodetic( geometry, maxSegmentLength, unit? ) -> [Geometry](../../guide/types/#geometry)

**[Since version 1.11](../../guide/version-matrix)**

Geodesically densifies geometries by inserting vertices to create segments no longer than the specified interval.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales. ** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`geometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The input geometry to be densified.
- **`maxSegmentLength`**: [Number](../../guide/types/#number)  
The maximum segment length allowed. Must be a positive value.
- **`unit`** (_Optional_): [Text](../../guide/types/#text) \| [Number](../../guide/types/#number)  
Measurement unit for maxSegmentLength. Defaults to the units of the input geometry. Use one of the string values listed in the [Units reference](https://developers.arcgis.com/arcade/function-reference/geometry_functions/#units-reference).

#### Return value: [Geometry](../../guide/types/#geometry)

![DensifyGeodetic_img](../images/geometry_functions/densifygeodetic.jpg)

#### Example

Returns the densified geometry with a maximum segment length of 10000

```arcade
DensifyGeodetic($feature, 10000, 'meters');
```


---------------------

## Difference

### Difference( geometry, subtractor ) -> [Geometry](../../guide/types/#geometry)

**[Since version 1.3](../../guide/version-matrix)**

Performs the topological difference operation for the two geometries. The resultant geometry comes from `inputGeometry`, not the `subtractor`. The dimension of `subtractor` has to be equal to or greater than that of `inputGeometry`.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`geometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The input geometry from which to subtract.
- **`subtractor`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The geometry to subtract from `geometry`.

#### Return value: [Geometry](../../guide/types/#geometry)

![Difference_img](../images/geometry_functions/difference.jpg)

#### Example

Subtracts the given polygon area from the feature.

```arcade
var subtractor = Polygon({ ... });
Difference($feature, subtractor);
```


---------------------

## Disjoint

### Disjoint( geometry1, geometry2 ) -> [Boolean](../../guide/types/#boolean)

**[Since version 1.3](../../guide/version-matrix)**

Indicates if one geometry is disjoint (doesn't intersect in any way) with another geometry. In the table below, the red highlight indicates that the function would return `true` with the specified geometries.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`geometry1`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The base geometry that is tested for the 'disjoint' relationship to `geometry2`.
- **`geometry2`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The comparison geometry that is tested for the 'disjoint' relationship to `geometry1`.

#### Return value: [Boolean](../../guide/types/#boolean)

![Disjoint_img](../images/geometry_functions/disjoint.jpg)

#### Example

Returns true if the geometries don't intersect

```arcade
var geom2 = Polygon({ ... });
Disjoint($feature, geom2);
```


---------------------

## Distance

### Distance( geometry1, geometry2, unit? ) -> [Number](../../guide/types/#number)

**[Since version 1.7](../../guide/version-matrix)**

Returns the planar distance between two geometries in the given units. This is a planar measurement using Cartesian mathematics.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`geometry1`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature) \| [Point[]](../../guide/types/#point)  
The geometry used to measure the distance from `geometry2`.
- **`geometry2`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature) \| [Point[]](../../guide/types/#point)  
The geometry used to measure the distance from `geometry1`.
- **`unit`** (_Optional_): [Text](../../guide/types/#text) \| [Number](../../guide/types/#number)  
Measurement unit of the return value. Use one of the string values listed in the [Units reference](https://developers.arcgis.com/arcade/function-reference/geometry_functions/#units-reference).

#### Return value: [Number](../../guide/types/#number)

#### Example

Returns the distance between two geometries in meters

```arcade
var geom2 = Point({ ... });
Distance($feature, geom2, 'meters')
```


---------------------

## DistanceGeodetic

### DistanceGeodetic( point1, point2, units? ) -> [Number](../../guide/types/#number)

**[Since version 1.8](../../guide/version-matrix)**

Calculates the shortest distance between two points along a great circle. Applies only to points with a Geographic Coordinate System (GCS) or the Web Mercator spatial reference. If the input points have a Projected Coordinate System (other than Web Mercator), you should use the [distance](../../function-reference/geometry_functions/#distance) method.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](https://developers.arcgis.com/arcade/function-reference/geometry_functions/).

#### Parameters

- **`point1`**: [Point](../../guide/types/#point) \| [Feature](../../guide/types/#feature)  
The point used to measure the distance from `point2`. This point must have a GCS or Web Mercator spatial reference.
- **`point2`**: [Point](../../guide/types/#point) \| [Feature](../../guide/types/#feature)  
The point used to measure the distance from `point1`. This point must have a GCS or Web Mercator spatial reference.
- **`units`** (_Optional_): [Text](../../guide/types/#text) \| [Number](../../guide/types/#number)  
Measurement unit of the return value. Use one of the string values listed in the [Units reference](https://developers.arcgis.com/arcade/function-reference/geometry_functions/#units-reference).

#### Return value: [Number](../../guide/types/#number)

#### Example

Returns the distance from a bus in a stream layer to the central station in kilometers

```arcade
var unionStation = Point({"x": -118.15, "y": 33.80, "spatialReference": { "wkid": 3857 }});
distanceGeodetic($feature, unionStation, 'kilometers');
```


---------------------

## EnvelopeIntersects

This function has 2 signatures:

- [EnvelopeIntersects( geometry1, geometry2 ) -> Boolean](#envelopeintersects1)
- [EnvelopeIntersects( features, envelope ) -> FeatureSet](#envelopeintersects2)

<a name="envelopeintersects1"></a>
### EnvelopeIntersects( geometry1, geometry2 ) -> [Boolean](../../guide/types/#boolean)

**[Since version 1.11](../../guide/version-matrix)**

Indicates if the envelope (or extent) of one geometry intersects the envelope of another geometry. In the graphic below, the red highlight indicates the scenarios where the function will return `true`.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`geometry1`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The geometry that is tested for the intersects relationship to the other geometry.
- **`geometry2`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The geometry being intersected.

#### Return value: [Boolean](../../guide/types/#boolean)

![EnvelopeIntersects_img](../images/geometry_functions/envelopeintersects.jpg)

#### Example

Returns true if the geometries intersect

```arcade
var geom2 = Polygon({ ... });
EnvelopeIntersects($feature, geom2);
```


<a name="envelopeintersects2"></a>
### EnvelopeIntersects( features, envelope ) -> [FeatureSet](../../guide/types/#featureset)

**[Since version 1.11](../../guide/version-matrix)**

Returns features from a FeatureSet where the envelopes (or extent) of a set of features intersect the envelope of another geometry. In the graphic below, the red highlight illustrates the spatial relationships where the function will return features.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
The FeatureSet that is tested for the intersects relationship to the input `envelope`.
- **`envelope`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The envelope being intersected.

#### Return value: [FeatureSet](../../guide/types/#featureset)

![EnvelopeIntersects_img](../images/geometry_functions/envelopeintersects.jpg)

#### Example

Returns the number of features that intersect the envelope of geom2

```arcade
var geom2 = Polygon({ ... });
Count( EnvelopeIntersects($layer, geom2) );
```


---------------------

## Equals

### Equals( geometry1, geometry2 ) -> [Boolean](../../guide/types/#boolean)

**[Since version 1.3](../../guide/version-matrix)**

Indicates if two geometries are equal, or geographically equivalent given the spatial reference and tolerance of the data. The two input geometries don't have to be clones to be considered equal.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`geometry1`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The first input geometry.
- **`geometry2`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The second input geometry.

#### Return value: [Boolean](../../guide/types/#boolean)

#### Example

Returns true if the geometries are equal

```arcade
var geom2 = Point({ ... });
Equals($feature, geom2);
```


---------------------

## Extent

### Extent( geometry ) -> [Extent](../../guide/types/#extent)

Constructs an Extent object from a JSON string or an object literal. The JSON schema must follow the [ArcGIS REST API format for Envelope geometries](http://resources.arcgis.com/en/help/arcgis-rest-api/#/Geometry_objects/02r3000000n1000000/). This function may also return the extent of an input Polygon, Point, Polyline or Multipoint.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameter

- **`geometry`**: [Dictionary](../../guide/types/#dictionary) \| [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The JSON or Geometry from which to construct the extent geometry object.

#### Return value: [Extent](../../guide/types/#extent)

#### Examples

```arcade
// Creates an Extent object
var extentJSON = {
  "xmin": -109.55, "ymin": 25.76, "xmax": -86.39, "ymax": 49.94,
  "spatialReference": { "wkid": 3857 }
};
Extent(extentJSON);
```

```arcade
// Returns the Extent of the given feature
Extent($feature)
```


---------------------

## Generalize

### Generalize( geometry, maxDeviation, removeDegenerateParts?, maxDeviationUnit? ) -> [Geometry](../../guide/types/#geometry)

**[Since version 1.11](../../guide/version-matrix)**

Reduces the number of vertices in the input geometry based on a given deviation value. Point and Multipoint geometries are left unchanged. Envelopes are converted to Polygons and then generalized.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`geometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The input geometry to be generalized.
- **`maxDeviation`**: [Number](../../guide/types/#number)  
The maximum allowed deviation from the generalized geometry to the original geometry.
- **`removeDegenerateParts`** (_Optional_): [Boolean](../../guide/types/#boolean)  
When `true` the degenerate parts of the geometry will be removed from the output (may be undesired for drawing).
- **`maxDeviationUnit`** (_Optional_): [Text](../../guide/types/#text) \| [Number](../../guide/types/#number)  
Measurement unit for maxDeviation. Defaults to the units of the input geometry. Use one of the string values listed in the [Units reference](https://developers.arcgis.com/arcade/function-reference/geometry_functions/#units-reference).

#### Return value: [Geometry](../../guide/types/#geometry)

![Generalize_img](../images/geometry_functions/generalize.jpg)

#### Example

Returns a generalized version of the input geometry

```arcade
// Removes vertices so segments are no more than 100 meters from the original geometry
Generalize($feature, 100, true, 'meters')
```


---------------------

## Geometry

### Geometry( feature ) -> [Geometry](../../guide/types/#geometry)

Constructs a Geometry object from a JSON string or an object literal. The JSON schema must follow the [ArcGIS REST API format for geometries](http://resources.arcgis.com/en/help/arcgis-rest-api/#/Geometry_objects/02r3000000n1000000/). This function may also return the Geometry of an input feature.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameter

- **`feature`**: [Feature](../../guide/types/#feature) \| [Dictionary](../../guide/types/#dictionary)  
The Feature or JSON from which to construct the geometry object.

#### Return value: [Geometry](../../guide/types/#geometry)

#### Examples

Returns the geometry of the feature

```arcade
Geometry($feature)
```

Constructs a point geometry. This can be done with any geometry type.

```arcade
var pointJSON = {"x": -118.15, "y": 33.80, "spatialReference": { "wkid": 4326 } };
Geometry(pointJSON);
```


---------------------

## Intersection

### Intersection( geometry1, geometry2 ) -> [Geometry](../../guide/types/#geometry)

**[Since version 1.3](../../guide/version-matrix)**

Constructs the set-theoretic intersection between two geometries and returns a new geometry.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`geometry1`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The geometry to intersect with `geometry2`.
- **`geometry2`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The geometry to intersect with `geometry1`.

#### Return value: [Geometry](../../guide/types/#geometry)

![Intersection_img](../images/geometry_functions/intersection.jpg)

#### Example

Returns the area common to both polygons

```arcade
var geom2 = Polygon({ ... });
Area(Intersection($feature, geom2), 'square-miles');
```


---------------------

## Intersects

This function has 2 signatures:

- [Intersects( geometry1, geometry2 ) -> Boolean](#intersects1)
- [Intersects( features, geometry ) -> FeatureSet](#intersects2)

<a name="intersects1"></a>
### Intersects( geometry1, geometry2 ) -> [Boolean](../../guide/types/#boolean)

**[Since version 1.3](../../guide/version-matrix)**

Indicates if one geometry intersects another geometry. In the graphic below, the red highlight indicates the scenarios where the function will return `true`.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`geometry1`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The geometry that is tested for the intersects relationship to `geometry2`.
- **`geometry2`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The geometry being intersected.

#### Return value: [Boolean](../../guide/types/#boolean)

![Intersects_img](../images/geometry_functions/intersects.jpg)

#### Example

Returns true if the geometries intersect

```arcade
var geom2 = Polygon({ ... });
Intersects($feature, geom2);
```


<a name="intersects2"></a>
### Intersects( features, geometry ) -> [FeatureSet](../../guide/types/#featureset)

**[Since version 1.3](../../guide/version-matrix)**

Returns features from a FeatureSet that intersect another geometry. In the graphic below, the red highlight illustrates the spatial relationships where the function will return features.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
The FeatureSet that is tested for the intersects relationship to `geometry`.
- **`geometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The geometry being intersected.

#### Return value: [FeatureSet](../../guide/types/#featureset)

![Intersects_img](../images/geometry_functions/intersects.jpg)

#### Example

Returns the number of features that intersect the polygon

```arcade
var geom2 = Polygon({ ... });
Count( Intersects($layer, geom2) );
```


---------------------

## IsSelfIntersecting

### IsSelfIntersecting( geometry ) -> [Boolean](../../guide/types/#boolean)

**[Since version 1.8](../../guide/version-matrix)**

Indicates whether the input geometry has rings, paths, or points that intersect or cross other parts of the geometry. For example, a single polyline feature whose paths intersect each other or a polygon with rings that self intersect would return `true`. 

#### Parameter

- **`geometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The polygon, polyline, or multipoint geometry to test for the self intersection.

#### Return value: [Boolean](../../guide/types/#boolean)

![IsSelfIntersecting_img](../images/geometry_functions/isselfintersecting.jpg)

#### Example

Returns true if the polyline's paths intersect each other

```arcade
var polyline = Polyline({ ... });
IsSelfIntersecting(polyline);
```


---------------------

## IsSimple

### IsSimple( geometry ) -> [Boolean](../../guide/types/#boolean)

**[Since version 1.11](../../guide/version-matrix)**

Indicates if the given geometry is topologically simple.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameter

- **`geometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The input geometry.

#### Return value: [Boolean](../../guide/types/#boolean)

#### Example

Returns true if the geometry is topologically simple

```arcade
IsSimple($feature);
```


---------------------

## Length

This function has 2 signatures:

- [Length( geometry, unit? ) -> Number](#length1)
- [Length( features, unit? ) -> Number](#length2)

<a name="length1"></a>
### Length( geometry, unit? ) -> [Number](../../guide/types/#number)

**[Since version 1.7](../../guide/version-matrix)**

Returns the length of the input geometry or Feature in the given units. This is a planar measurement using Cartesian mathematics.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`geometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature) \| Points[]  
The geometry or geometries for which to calculate the planar length.
- **`unit`** (_Optional_): [Text](../../guide/types/#text) \| [Number](../../guide/types/#number)  
Measurement unit of the return value. Use one of the string values listed in the [Units reference](https://developers.arcgis.com/arcade/function-reference/geometry_functions/#units-reference).

#### Return value: [Number](../../guide/types/#number)

#### Example

Returns the planar length of the feature in kilometers

```arcade
Length($feature, 'kilometers')
```


<a name="length2"></a>
### Length( features, unit? ) -> [Number](../../guide/types/#number)

**[Since version 1.7](../../guide/version-matrix)**

Returns the length of the input FeatureSet in the given units. This is a planar measurement using Cartesian mathematics.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
The FeatureSet for which to calculate the planar length.
- **`unit`** (_Optional_): [Text](../../guide/types/#text) \| [Number](../../guide/types/#number)  
Measurement unit of the return value. Use one of the string values listed in the [Units reference](https://developers.arcgis.com/arcade/function-reference/geometry_functions/#units-reference).

#### Return value: [Number](../../guide/types/#number)

#### Example

Returns the planar length of the layer in meters

```arcade
Length($layer, 'meters')
```


---------------------

## Length3D

This function has 2 signatures:

- [Length3D( geometry, unit? ) -> Number](#length3d1)
- [Length3D( features, unit? ) -> Number](#length3d2)

<a name="length3d1"></a>
### Length3D( geometry, unit? ) -> [Number](../../guide/types/#number)

**[Since version 1.14](../../guide/version-matrix)**

**Profiles**: [Attribute Rules](../../guide/profiles/#attribute-rules) | [Popups](../../guide/profiles/#popups) | [Field Calculation](../../guide/profiles/#field-calculation) | [Tasks](../../guide/profiles/#tasks)

Returns the planar (i.e. Cartesian) length of the input geometry or Feature taking height or Z information into account. The geometry provided to this function must be assigned a projected coordinate system. If the spatial reference does not provide a value for Z units, then the result will be returned in meters. Keep in mind that not all clients (such as the 3.x series of the ArcGIS API for JavaScript) support requesting Z values even when the data contains Z information.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`geometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature) \| Points[]  
The geometry or Feature for which to calculate the planar length in 3D space.
- **`unit`** (_Optional_): [Text](../../guide/types/#text) \| [Number](../../guide/types/#number)  
Measurement unit of the return value. Use one of the string values listed in the [Units reference](https://developers.arcgis.com/arcade/function-reference/geometry_functions/#units-reference).

#### Return value: [Number](../../guide/types/#number)

#### Examples

Returns the 3D planar length of the feature in the unit of the spatial reference of the context executing the expression.

```arcade
Length3D($feature)
```

Returns the 3D planar length of the feature in feet.

```arcade
Length3D($feature, 'feet')
```


<a name="length3d2"></a>
### Length3D( features, unit? ) -> [Number](../../guide/types/#number)

**[Since version 1.14](../../guide/version-matrix)**

**Profiles**: [Attribute Rules](../../guide/profiles/#attribute-rules) | [Popups](../../guide/profiles/#popups) | [Field Calculation](../../guide/profiles/#field-calculation) | [Tasks](../../guide/profiles/#tasks)

Returns the planar (i.e. Cartesian) length of the input FeatureSet taking height or Z information into account. The geometry provided to this function must be assigned a projected coordinate system. If the spatial reference does not provide a value for Z units, then the result will be returned in meters. Keep in mind that not all clients (such as the 3.x series of the ArcGIS API for JavaScript) support requesting Z values even when the data contains Z information.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
The FeatureSet for which to calculate the planar length in 3D space.
- **`unit`** (_Optional_): [Text](../../guide/types/#text) \| [Number](../../guide/types/#number)  
Measurement unit of the return value. Use one of the string values listed in the [Units reference](https://developers.arcgis.com/arcade/function-reference/geometry_functions/#units-reference).

#### Return value: [Number](../../guide/types/#number)

#### Example

Returns the 3D length of the layer's features in meters

```arcade
Length($layer, 'meters')
```


---------------------

## LengthGeodetic

This function has 2 signatures:

- [LengthGeodetic( geometry, unit? ) -> Number](#lengthgeodetic1)
- [LengthGeodetic( features, unit? ) -> Number](#lengthgeodetic2)

<a name="lengthgeodetic1"></a>
### LengthGeodetic( geometry, unit? ) -> [Number](../../guide/types/#number)

**[Since version 1.7](../../guide/version-matrix)**

Returns the geodetic length of the input geometry or Feature in the given units. This is more reliable measurement of length than [Length()](../../function-reference/geometry_functions/#length) because it takes into account the Earth's curvature. Support is limited to geometries with a Web Mercator (wkid 3857) or a WGS 84 (wkid 4326) spatial reference.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](https://developers.arcgis.com/arcade/function-reference/geometry_functions/).

#### Parameters

- **`geometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature) \| Points[]  
The geometry for which to calculate the geodetic length.
- **`unit`** (_Optional_): [Text](../../guide/types/#text) \| [Number](../../guide/types/#number)  
Measurement unit of the return value. Use one of the string values listed in the [Units reference](https://developers.arcgis.com/arcade/function-reference/geometry_functions/#units-reference).

#### Return value: [Number](../../guide/types/#number)

#### Example

Returns the geodetic length of the feature in kilometers

```arcade
LengthGeodetic($feature, 'kilometers')
```


<a name="lengthgeodetic2"></a>
### LengthGeodetic( features, unit? ) -> [Number](../../guide/types/#number)

**[Since version 1.7](../../guide/version-matrix)**

Returns the geodetic length of the input FeatureSet in the given units. This is more reliable measurement of length than [Length()](../../function-reference/geometry_functions/#length) because it takes into account the Earth's curvature. Support is limited to geometries with a Web Mercator (wkid 3857) or a WGS 84 (wkid 4326) spatial reference.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](https://developers.arcgis.com/arcade/function-reference/geometry_functions/).

#### Parameters

- **`features`**: [FeatureSet](../../guide/types/#featureset)  
The FeatureSet for which to calculate the geodetic length.
- **`unit`** (_Optional_): [Text](../../guide/types/#text) \| [Number](../../guide/types/#number)  
Measurement unit of the return value. Use one of the string values listed in the [Units reference](https://developers.arcgis.com/arcade/function-reference/geometry_functions/#units-reference).

#### Return value: [Number](../../guide/types/#number)

#### Example

Returns the geodetic length of the layer in meters

```arcade
LengthGeodetic($layer, 'meters')
```


---------------------

## MultiPartToSinglePart

### MultiPartToSinglePart( geometry ) -> [Geometry[]](../../guide/types/#geometry)

**[Since version 1.3](../../guide/version-matrix)**

Converts a multi-part geometry into separate geometries.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameter

- **`geometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The multi-part geometry to break into single parts.

#### Return value: [Geometry[]](../../guide/types/#geometry)

![MultiPartToSinglePart_img](../images/geometry_functions/multiparttosinglepart.jpg)

#### Example

Returns an array of single-part geometries from a multi-part geometry

```arcade
var allParts = MultiPartToSinglePart($feature)
```


---------------------

## Multipoint

### Multipoint( definition ) -> [Multipoint](../../guide/types/#multipoint)

Constructs a Multipoint object from a JSON string or an object literal. The JSON schema must follow the [ArcGIS REST API format for multipoint geometries](http://resources.arcgis.com/en/help/arcgis-rest-api/#/Geometry_objects/02r3000000n1000000/)

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameter

- **`definition`**: [Dictionary](../../guide/types/#dictionary)  
The JSON from which to construct the multipoint geometry object.

#### Return value: [Multipoint](../../guide/types/#multipoint)

#### Example

```arcade
// Creates a Multipoint object
var multipointJSON = {
  "points": [[-97.06138,32.837],[-97.06133,32.836],[-97.06124,32.834],[-97.06127,32.832]],
  "spatialReference" : { "wkid": 3857 }
};
Multipoint(multipointJSON);
```


---------------------

## Offset

### Offset( geometry, offsetDistance, offsetUnit?, joinType?, bevelRatio?, flattenError? ) -> [Geometry](../../guide/types/#geometry)

**[Since version 1.11](../../guide/version-matrix)**

Creates a geometry that is a constant planar distance from an input geometry. It is similar to buffering, but produces a one-sided result.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`geometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The geometry to offset. Point geometries are not supported.
- **`offsetDistance`**: [Number](../../guide/types/#number)  
The planar distance to offset from the input geometry. If `offsetDistance > 0`, then the offset geometry is constructed to the right of the input geometry, if `offsetDistance = 0`, then there is no change in the geometries, otherwise it is constructed to the left. The direction of the paths or rings of the input geometry determines which side of the geometry is considered right, and which side is considered left. For a simple polygon, the orientation of outer rings is clockwise and for inner rings it is counter clockwise. So the right side of a simple polygon is always its inside.
- **`offsetUnit`** (_Optional_): [Text](../../guide/types/#text) \| [Number](../../guide/types/#number)  
Measurement unit for `offsetDistance`. Defaults to the units of the input geometry. Use one of the string values listed in the [Units reference](https://developers.arcgis.com/arcade/function-reference/geometry_functions/#units-reference).
- **`joinType`** (_Optional_): [Text](../../guide/types/#text)  
The join type. Possible values are `round`, `bevel`, `miter`, or `square`.
- **`bevelRatio`** (_Optional_): [Number](../../guide/types/#number)  
Applicable when `joinType = 'miter'`; `bevelRatio` is multiplied by the offset distance and the result determines how far a mitered offset intersection can be located before it is beveled.
- **`flattenError`** (_Optional_): [Number](../../guide/types/#number)  
Applicable when `joinType = 'round'`; `flattenError` determines the maximum distance of the resulting segments compared to the true circular arc. The algorithm never produces more than around 180 vertices for each round join.

#### Return value: [Geometry](../../guide/types/#geometry)

![Offset_img](../images/geometry_functions/offset.jpg)

#### Example

Returns the offset geometry

```arcade
Offset($feature, 10, 'meters', 'square');
```


---------------------

## Overlaps

This function has 2 signatures:

- [Overlaps( geometry1, geometry2 ) -> Boolean](#overlaps1)
- [Overlaps( overlappingFeatures, geometry ) -> FeatureSet](#overlaps2)

<a name="overlaps1"></a>
### Overlaps( geometry1, geometry2 ) -> [Boolean](../../guide/types/#boolean)

**[Since version 1.3](../../guide/version-matrix)**

Indicates if one geometry overlaps another geometry. In the graphic below, the red highlight indicates the scenarios where the function will return `true`.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`geometry1`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The base geometry that is tested for the 'overlaps' relationship with `geometry2`.
- **`geometry2`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The comparison geometry that is tested for the 'overlaps' relationship with `geometry1`.

#### Return value: [Boolean](../../guide/types/#boolean)

![Overlaps_img](../images/geometry_functions/overlaps.jpg)

#### Example

Returns true if the geometries overlap

```arcade
var geom2 = Polygon({ ... });
Overlaps($feature, geom2);
```


<a name="overlaps2"></a>
### Overlaps( overlappingFeatures, geometry ) -> [FeatureSet](../../guide/types/#featureset)

**[Since version 1.3](../../guide/version-matrix)**

Returns features from a FeatureSet that overlap another geometry. In the graphic below, the red highlight illustrates the spatial relationships where the function will return features.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`overlappingFeatures`**: [FeatureSet](../../guide/types/#featureset)  
The features that are tested for the 'overlaps' relationship with `geometry`.
- **`geometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The comparison geometry that is tested for the 'overlaps' relationship with `overlappingFeatures`.

#### Return value: [FeatureSet](../../guide/types/#featureset)

![Overlaps_img](../images/geometry_functions/overlaps.jpg)

#### Example

Returns the number of features that overlap the polygon

```arcade
var geom2 = Polygon({ ... });
Count( Overlaps($layer, geom2) );
```


---------------------

## Point

### Point( definition ) -> [Point](../../guide/types/#point)

Constructs a Point object from a JSON string or an object literal. The JSON schema must follow the [ArcGIS REST API format for Point geometries](http://resources.arcgis.com/en/help/arcgis-rest-api/#/Geometry_objects/02r3000000n1000000/).

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameter

- **`definition`**: [Dictionary](../../guide/types/#dictionary)  
The JSON from which to construct the point geometry object.

#### Return value: [Point](../../guide/types/#point)

#### Example

```arcade
// Creates a Point object
var pointJSON = { "x": -118.15, "y": 33.80, "spatialReference": { "wkid": 4326 }};
Point(pointJSON)
```


---------------------

## Polygon

### Polygon( definition ) -> [Polygon](../../guide/types/#polygon)

Constructs a Polygon object from a JSON string or an object literal. The JSON schema must follow the [ArcGIS REST API format for Polygon geometries](http://resources.arcgis.com/en/help/arcgis-rest-api/#/Geometry_objects/02r3000000n1000000/).

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameter

- **`definition`**: [Dictionary](../../guide/types/#dictionary)  
The JSON from which to construct the polygon geometry object.

#### Return value: [Polygon](../../guide/types/#polygon)

#### Example

```arcade
// Creates a Polygon object
var polygonJSON = {
  "rings": [
    [[-97.06138,32.837],[-97.06133,32.836],[-97.06124,32.834],[-97.06127,32.832], [-97.06138,32.837]],
    [[-97.06326,32.759],[-97.06298,32.755],[-97.06153,32.749], [-97.06326,32.759]]
  ],
  "spatialReference": { "wkid": 3857 }
};
Polygon(polygonJSON);
```


---------------------

## Polyline

### Polyline( definition ) -> [Polyline](../../guide/types/#polyline)

Constructs a Polyline object from a JSON string or an object literal. The JSON schema must follow the [ArcGIS REST API format for Polyline geometries](http://resources.arcgis.com/en/help/arcgis-rest-api/#/Geometry_objects/02r3000000n1000000/).

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameter

- **`definition`**: [Dictionary](../../guide/types/#dictionary)  
The JSON from which to construct the polyline geometry object.

#### Return value: [Polyline](../../guide/types/#polyline)

#### Example

```arcade
// Creates a Polyline object
var polylineJSON = {
  "paths": [
    [[-97.06138,32.837],[-97.06133,32.836],[-97.06124,32.834],[-97.06127,32.832]],
    [[-97.06326,32.759],[-97.06298,32.755]]
  ],
  "spatialReference": { "wkid": 4326 }
};
Polyline(polylineJSON);
```


---------------------

## Relate

### Relate( geometry1, geometry2, relation ) -> [Boolean](../../guide/types/#boolean)

**[Since version 1.11](../../guide/version-matrix)**

Indicates if the given DE-9IM relation is `true` for the two geometries.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`geometry1`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The first geometry for the relation.
- **`geometry2`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The second geometry for the relation.
- **`relation`**: [Text](../../guide/types/#text)  
The Dimensionally Extended 9 Intersection Model (DE-9IM) matrix relation (encoded as a string) to test against the relationship of the two geometries. This string contains the test result of each intersection represented in the DE-9IM matrix. Each result is one character of the string and may be represented as either a number (maximum dimension returned: 0,1,2), a Boolean value (T or F), or a mask character (for ignoring results: '\*').

Example: Each of the following DE-9IM string codes are valid for testing whether a polygon geometry completely contains a line geometry: TTTFFTFFT (Boolean), 'T\*\*\*\*\*\*FF\*' (ignore irrelevant intersections), or '102FF\*FF\*' (dimension form). Each returns the same result.

#### Return value: [Boolean](../../guide/types/#boolean)

#### Example

Returns true if the relation of the input geometries matches

```arcade
Relate($feature, geometry2, 'TTTFFTFFT')
```


---------------------

## RingIsClockwise

### RingIsClockwise( points ) -> [Boolean](../../guide/types/#boolean)

**[Since version 1.7](../../guide/version-matrix)**

Indicates whether the points in a polygon ring are ordered in a clockwise direction.

#### Parameter

- **`points`**: [Array](../../guide/types/#array)  
An array of points in a polygon ring.

#### Return value: [Boolean](../../guide/types/#boolean)

#### Example

```arcade
// $feature is a polygon feature
var polygonRings = Geometry($feature).rings;
IIf(RingIsClockwise(polygonRings[0]), 'correct polygon', 'incorrect direction')
```


---------------------

## Rotate

### Rotate( geometry, angle, rotationOrigin? ) -> [Geometry](../../guide/types/#geometry)

**[Since version 1.11](../../guide/version-matrix)**

Rotates a geometry counterclockwise by the specified number of degrees. Rotation is around the centroid, or a given rotation point.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`geometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The geometry to rotate.
- **`angle`**: [Number](../../guide/types/#number)  
The rotation angle in degrees.
- **`rotationOrigin`** (_Optional_): [Point](../../guide/types/#point)  
Point to rotate the geometry around. Defaults to the centroid of the geometry.

#### Return value: [Geometry](../../guide/types/#geometry)

![Rotate_img](../images/geometry_functions/rotate.jpg)

#### Example

Returns the input feature rotated about the centroid by 90 degrees

```arcade
Rotate($feature, 90)
```


---------------------

## SetGeometry

### SetGeometry( feature, geometry ) -> Null

**[Since version 1.3](../../guide/version-matrix)**

Sets or replaces a geometry on a user-defined Feature. Note that features referenced as global variables are immutable; their geometries cannot be changed.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`feature`**: [Feature](../../guide/types/#feature)  
A feature whose geometry will be updated.
- **`geometry`**: [Geometry](../../guide/types/#geometry)  
The geometry to set on the input feature.

#### Return value: Null

#### Example

Sets a new geometry on the feature

```arcade
var pointFeature = Feature(Point( ... ), 'name', 'buffer centroid');
var mileBuffer = BufferGeodetic(Geometry(pointFeature), 1, 'mile');
SetGeometry(pointFeature, mileBuffer);
```


---------------------

## Simplify

### Simplify( geometry ) -> [Geometry](../../guide/types/#geometry)

**[Since version 1.11](../../guide/version-matrix)**

Performs the simplify operation on the geometry. This alters the given geometry to make it topologically legal.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameter

- **`geometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The geometry to be simplified.

#### Return value: [Geometry](../../guide/types/#geometry)

#### Example

Returns the simplified geometry of the feature

```arcade
Simplify($feature);
```


---------------------

## SymmetricDifference

### SymmetricDifference( leftGeometry, rightGeometry ) -> [Geometry](../../guide/types/#geometry)

**[Since version 1.3](../../guide/version-matrix)**

Performs the Symmetric difference operation on the two geometries. The symmetric difference includes the parts of both geometries that are not common with each other.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`leftGeometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The geometry instance to compare to `rightGeometry` in the XOR operation.
- **`rightGeometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The geometry instance to compare to `leftGeometry` in the XOR operation.

#### Return value: [Geometry](../../guide/types/#geometry)

![SymmetricDifference_img](../images/geometry_functions/symmetricdifference.jpg)

#### Example

Returns a polygon representing areas where both inputs do not overlap

```arcade
var geom2 = Polygon({ ... });
SymmetricDifference($feature, geom2);
```


---------------------

## Touches

This function has 2 signatures:

- [Touches( geometry1, geometry2 ) -> Boolean](#touches1)
- [Touches( touchingFeatures, geometry ) -> FeatureSet](#touches2)

<a name="touches1"></a>
### Touches( geometry1, geometry2 ) -> [Boolean](../../guide/types/#boolean)

**[Since version 1.3](../../guide/version-matrix)**

Indicates if one geometry touches another geometry. In the graphic below, the red highlight indicates the scenarios where the function will return `true`.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`geometry1`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The geometry to test the 'touches' relationship with `geometry2`.
- **`geometry2`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The geometry to test the 'touches' relationship with `geometry1`.

#### Return value: [Boolean](../../guide/types/#boolean)

![Touches_img](../images/geometry_functions/touches.jpg)

#### Example

Returns true if the geometries touch

```arcade
var geom2 = Polygon({ ... });
Touches($feature, geom2);
```


<a name="touches2"></a>
### Touches( touchingFeatures, geometry ) -> [FeatureSet](../../guide/types/#featureset)

**[Since version 1.3](../../guide/version-matrix)**

Returns features from a FeatureSet that touch another geometry. In the graphic below, the red highlight illustrates the spatial relationships where the function will return features.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`touchingFeatures`**: [FeatureSet](../../guide/types/#featureset)  
The features to test the 'touches' relationship with `geometry`.
- **`geometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The geometry to test the 'touches' relationship with `touchingFeatures`.

#### Return value: [FeatureSet](../../guide/types/#featureset)

![Touches_img](../images/geometry_functions/touches.jpg)

#### Example

Returns the number of features in the layer that touch the geometry.

```arcade
var geom = Polygon({ ... });
Count( Touches($layer, geom) );
```


---------------------

## Union

### Union( geometries ) -> [Geometry](../../guide/types/#geometry)

**[Since version 1.3](../../guide/version-matrix)**

Constructs the set-theoretic union of the geometries in an input array, or list, and returns a single Geometry. All inputs must have the same geometry type and share the same spatial reference.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameter

- **`geometries`**: [Geometry[]](../../guide/types/#geometry) \| [Feature[]](../../guide/types/#feature)  
An array, or list, of geometries to union into a single geometry. This can be any number of geometries.

#### Return value: [Geometry](../../guide/types/#geometry)

![Union_img](../images/geometry_functions/union.jpg)

#### Examples

Unions geometries passed as an array

```arcade
var geom2 = Polygon({ ... });
Union([ $feature, geom2 ]);
```

Unions geometries passed as a list

```arcade
var geom2 = Polygon({ ... });
var geom3 = Polygon({ ... });
var geom4 = Polygon({ ... });
Union(Geometry($feature), geom2, geom3, geom4);
```


---------------------

## Within

This function has 2 signatures:

- [Within( innerGeometry, outerGeometry ) -> Boolean](#within1)
- [Within( innerGeometry, outerFeatures ) -> FeatureSet](#within2)

<a name="within1"></a>
### Within( innerGeometry, outerGeometry ) -> [Boolean](../../guide/types/#boolean)

**[Since version 1.7](../../guide/version-matrix)**

Indicates if one geometry is within another geometry. In the graphic below, the red highlight indicates the scenarios where the function will return `true`.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`innerGeometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The base geometry that is tested for the 'within' relationship to `outerGeometry`.
- **`outerGeometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The comparison geometry that is tested for the 'contains' relationship to `innerGeometry`.

#### Return value: [Boolean](../../guide/types/#boolean)

![Within_img](../images/geometry_functions/within.jpg)

#### Example

Returns true if the feature is within the given polygon

```arcade
var outerGeom = Polygon({ ... });
Within($feature, outerGeom);
```


<a name="within2"></a>
### Within( innerGeometry, outerFeatures ) -> [FeatureSet](../../guide/types/#featureset)

**[Since version 1.7](../../guide/version-matrix)**

Returns features from a FeatureSet that are within another geometry. In the graphic below, the red highlight illustrates the spatial relationships where the function will return features.

**Be aware that using `$feature` as input to this function will yield results only as precise as the view's scale resolution. Therefore values returned from expressions using this function may change after zooming between scales.** [Read more here](../../function-reference/geometry_functions/).

#### Parameters

- **`innerGeometry`**: [Geometry](../../guide/types/#geometry) \| [Feature](../../guide/types/#feature)  
The base geometry that is tested for the 'within' relationship to `outerFeatures`.
- **`outerFeatures`**: [FeatureSet](../../guide/types/#featureset)  
The comparison features that are tested for the 'contains' relationship to `innerGeometry`.

#### Return value: [FeatureSet](../../guide/types/#featureset)

![Within_img](../images/geometry_functions/within.jpg)

#### Example

Returns the number of features in the layer within the polygon

```arcade
var outerGeom = Polygon({ ... });
Count( Within(outerGeom, $layer) );
```


---------------------