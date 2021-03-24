tags: #JavaScript #data-type #modern-js #english
related: [[210207 Arrays]] | [[210210 Array methods pt.2]]

<hr />

## Array methods

## Add / Remove items
We've seen couple methods that add/remove in the previous chapter (check the related post).

This chapter introduces few other methods.

### splice
We can use `delete` to delete an element from the array.
```js
let arr = ["My", "name", "is", "Eu", "Eubug"];

delete arr[3]; // remove "Eu"

console.log( arr[3] ); // undefined

console.log( arr ); // ["My", "name", "is", , "Eubug"]

console.log( arr.length ); // still 5
```

As you can see from the `arr.length`, we didn't actually remove the space that item was occupied; we just set it to undefined. What we actually want is, delete the value and its space. We can use `splice`.

The syntax:
```js
arr.splice( start [, deleteN, elem1, ..., elemN])
```

- it modifies the `arr`.
- starting from the index `start`, it replaces `deleteN` items with `elem1, ...., elemN` at their place. If `elem1, ..., elemN` is not  provided, it simply removes the item from the list.
- negative indexes are allowed; it specifies the position from the end of the array.
- returns the array of removed elements.

```js
let arr = ["My", "name", "is", "Eu", "Eubug"];

arr.splice(3, 1); // delete "Eu"

console.log( arr[3] ); // Eubug

console.log( arr ); // ["My", "name", "is", "Eubug"]

console.log( arr.length ); // 4
```

We can also insert elements without removing any. Just set `deleteN` to `0`.

### silce

The syntax:
```js
arr.slice([start], [end])
```

It creates a subarray from `start` to `end` (not including it).

It is similar to `string.slice` except that `arr.silce` create subarrays instead of substrings.

As you can see from the syntax, both boundaries are optional. When both are omitted, it creates a copy of the original array which is often used.

```js
let arr = [1, 2, 3];
let copy = arr.slice();
copy[2] = 5;

console.log( arr );  // [1, 2, 3]
console.log( copy ); // [1, 2, 5]
```

### concat
the syntax:
```js
arr.concat(arg1, arg2, ...)
```

- does not modify the `arr`.
- accepts any values or arrays.
- if no argument is given, the array itself is copied.

### Symbol.isConcatSpreadable
When you `concat` an object, it will add the object as a whole:
```js
let arrayLike = {
	0: "something",
	length: 1,
};

console.log( [1].concat( arrayLike ) ); // [1, {0: "something", length: 1}]
```

To copy over values only, you can add `Symbol.isConcatSpreadable` property:
```js
let arrayLike = {
	0: "something",
	1: "else",
	[Symbol.isConcatSpreadable]: true,
	length: 2,
};

console.log( [1].concat( arrayLike ) ); // [1, 'something', 'else']
```

## Reference
- https://javascript.info/array-methods