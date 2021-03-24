tags: #JavaScript #data-type #modern-js #english
related: [[210207 Arrays]] | [[210208 Array methods pt.1]]

<hr />

## Array methods

## Iterate: forEach

We can use `arr.forEach` method to run a function for every element of the array.

```js
arr.forEach(function(item, index, array)) {
	// ... do something
}
```

For example, we can call `alert` on every element.
```js
arr = [1, 2, 3];
arr.forEach(alert); 
```

Or we can be more specific:
```js
arr = ["apple", "banana", "carrot"]

arr.forEach((item, inedx, arr) => {
	console.log( `${item} is at index ${index} in ${array}` );
})
```

## Searching in array
### indexOf | lastIndexOf | includes
These methods all have the same syntax.
- `arr.indexOf(item, from)` - looks for `item` starting from index `from`, and returns the index where it was found, otherwise `-1`
- `arr.lastIndexOf(item, from)` - same, but starts from the array end.
- `arr.includes(item, from)` - looks for `item` starting from index `from`. return `true` if found.

```js
let arr = [1, 0, false];

console.log( arr.indexOf(0) ); // 1
console.log( arr.indexOf(false) ); // 2
console.log( arr.indexOf(null) ); // -1

console.log( arr.includes(1) ); // true
```

These methods use `===` comparison. So, when it looks for `false`, it will exactly look for `false` not the zero.

#### which methods should we use?
- For the inclusion check, use `includes`.
- If you want these find methods to handle `NaN` correctly, use `includes`.
- If you want to know the exact index, use `indexOf` or `lastIndexOf`.

```js
const arr = [NaN];
console.log( arr.indexOf(NaN) ); // -1 (should be 0)
console.log( arr.includes(NaN) ); // true (correct)
```

### find and findIndex
To find an object with the specific condition, use `arr.find(fn)`.

The syntax:
```js
let result = arr.find(function(item, index, array) {
	// if true is returned, item is returned and iteration is stopped
	// returns undefined if nothing found
});
```

- `item` is the element.
- `index` is its index.
- `array` is the array itself.

```js
let users = [
	{id: 1, name: "John"},
	{id: 2, name: "Pete"},
	{id: 3, name: "Mary"}
];

let user = users.find(item => item.id < 3);

console.log(user.name); // John
```

As you can see from the above example, we can ignore other arguments and only use `item` which is very common. Also keep in mind that `arr.find(fn)` stops iterating once it finds `true`; so only `"John"` is returned although there are `"Pete"` and `"Mary"` whose `item.id < 3`.

`arr.findIndex` is same except that it returns the index not the element itself. In falsy scenario it returns `-1`.

### filter
The `arr.find(fn)` looks for the first element that meets our condition. If there are many, we can use `arr.filter(fn)`. It returns an array of all matching elements.
```js
let results = arr.filter(function(item, index, array) {
	// if true item is pushed to results and the iteration continues
	// returns empty array if nothing found
});
```

For example:
```js
let users = [
	{id: 1, name: "John"},
	{id: 2, name: "Pete"},
	{id: 3, name: "Mary"}
];

let someUsers = users.filter(item => item.id < 3);
console.log( someUsers.length); // 2
```

## Transform an array

### map
- one of the most useful and often used method.
- it calls the function for each element of the array and returns the array of results.

The syntax:

```js
let result = arr.map(function(item, inedx, array) {
	// returns the new value instead of item; 
});
```

For example, here we transform each element into its length:

```js
let lengths = ["Bilbo", "Gandalf", "Nazgul"].map(item => item.length);
console.log(lengths); // 5, 7, 6
```

### sort(fn)
The method `sort(fn)` sorts the array *in place*, changing its element order and returns the sorted array; the returned value is usually ignored.

**The items are sorted as strings by default.**

```js
let arr = [1, 2, 15];
arr.sort();

console.log( arr ); // 1, 15, 2
```

We can pass in a function as an argument in `sort()` to supply our own sorting order.

```js
function compare(a, b) {
	if (a > b) return 1;
	if (a == b) return 0;
	if (a < b) return -1;
}

let arr = [1, 2, 15];

arr.sort(compare);

console.log(arr); // 1, 2, 15
```

#### A comparison function may return any number
A comparison function only required to return a positive number to say "greater" and a negative number to say "less".

So we can modify our `compare` function for numeric values like the below and it will work as we intended:
```js
function compare(a, b) {
	return a - b;
}

let arr = [1, 2, 15];

arr.sort(compare);

console.log(arr); // 1, 2, 15

```

or just use the arrow function:

```js
arr.sort( (a, b) => a - b);
```

### reverse
The `reverse` method reverses the order of elements in `arr`.

```js
let arr = [1, 2, 3, 4, 5];
arr.reverse

console.log( arr ); // 5, 4, 3, 2, 1
```

It also returns the array after the reversal but is normally ignored since the original array is modified.

### split and join
The `str.split(delim)` method is used to split the string into an array by the given delimiter `delim`.

```js
let names = "Alex, Bean, Chris";

let arr = names.split(', ');

for (let name of arr) {
	console.log(`A message to ${name}.`);
}
```

We can use the optional second argument in `str.split(delim, len)` to limit the array length to `len`.

We can split the string into an array of letters:
```js
let str = "Eubug";
console.log( str.split('') ); // ["E", "u", "b", "u", "g"]
```

---

The method `arr.join(glue)` creates a string of `arr` items joined by `glue` between them.

For instance:
```js
let arr = ["Apple", "Banana", "Carrot"];
let str = arr.join('-');
console.log(str); // Apple-Banana-Carrot
```

### reduce | reduceRight

We use `reduce` and `reduceRight` to calculate a single value based on the array.

The syntax:
```js
let value = arr.reduce(function(accumulator, item, index, array) {
	// ...
}, [inditial]);
```

- `accumulator` is the result of the previous function call (equals `initial` the first time - if provided).
- `item` is the current array item.
- `index` is its position.
- `array` is the array.

For example, we can use `reduce` to get a sum of an array:
```js
let arr = [1, 2, 3, 4, 5];
the result = arr.reduce((sum, current) => sum + current, 0);
console.log(result); // 15
```

The `arr.reduceRight` does the same except that it goes from right to left.

## Array.isArray
We cannot use `typeof` to distinguish arrays in JavaScript since they're just an object.

```js
console.log( typeof({}) ); // object
console.log( typeof([]) ); // same
```

Instead, we can use `isArray()` in Array.

```js
console.log(Array.isArray({})); // false
console.log(Array.isArray([])); // true
```

## Most methods support "thisArg"

Almost all array methods that call functions provide an optional additional parameter `thisArg`. The value of `thisArg` becomes `this` for `func`.

This is rarely used.