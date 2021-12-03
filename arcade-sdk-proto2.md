### All( array, testFunction ) -> `Boolean`

**[Since version 1.16](../../guide/version-matrix)**

Indicates whether all of the elements in a given array pass a test from the provided function. Returns `true` if the function returns `true` for all items in the input array.

#### Parameters

**`array`**: [Array](../../guide/types/#array)

The input array to test.

**`testFunction`**: [Function](../../guide/logic/#user-defined-functions)

The function used to test each element in the `inputArray`. The function must return a truthy value if the element passes the test. The functioncan be a user-defined function or a core Arcade function defined with the following parameters:

&nbsp;&nbsp;**`value`**  
&nbsp;&nbsp;Represents the value of an element in the array.

#### Returns value

[Boolean](../../guide/types/#boolean). `true` if the test function returns a truthy value for all the element.

#### Example

Returns `false` because some of the elements in the input array do not pass the `isEven` test

```arcade
// isEven is used to test if each element in the array is even
// it returns true if the element is divisible by two, false if is not
function isEven(value) { return value % 2 == 0 }
// The isEven function will execute for each element in the array,
// returning the following values: false, true, false, true, false
// Since some of the values in the array did not pass the test
// (return true), the return value will be false
Any([1,2,3,4,5], isEven)
```

Uses the existing `isEmpty` Arcade function as the `testFunction`. This is valid because `isEmpty` takes a single parameter and returns a boolean value. This expression returns `true` if all of the fields are empty.

```arcade
var myArray = [ $feature.field1, $feature.field2, $feature.field3, $feature.field4];
All(myArray, isEmpty)
```
