# TC39 proposal: reduce() single callback behavior

## Intro

The behavior of the reduce callback does not really need to change if an initial value is not provided - especially as we have default parameters.

## Background

Reduce syntax:

```javascript
arr.reduce(callback[, initialValue])
```

>The first time the callback is called, previousValue and currentValue can be one of two values. If initialValue is provided in the call to reduce, then previousValue will be equal to initialValue and currentValue will be equal to the first value in the array. _If no initialValue was provided, then previousValue will be equal to the first value in the array and currentValue will be equal to the second._

-[MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce#Description)

This proposal suggests, if no initialValue was provided, then the previous value will be `undefined`.

**At the heart of this proposal is making `reduce` always behave the same way.**


## Problem

TL;DR: It would be nice if the function would treat default params, as if the `initialValue` was set

```javascript
var ar = [{v:1}, {v:2}];

result1 = ar.reduce(
  (p,c) => p+c.v,
  0
);

console.log(result1);
/*
output: 3

*/


result2 = ar.reduce(
  ((p=0,c) => p+c.v)
);

console.log(result2);
/*
output expected: 3
output actual: "[object Object]2"
*/

```

## Example

http://codepen.io/AshCoolman/pen/aveOrL
