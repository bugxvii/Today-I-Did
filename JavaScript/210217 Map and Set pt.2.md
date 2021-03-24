tags: #JavaScript #data-type #modern-js #english
related: [[210216 Map and Set pt.1]]

---

## Object.entries: Map from Object

We can pass an array (or another iterable) with key/value pairs as an element (or data) of the map when we create one:
```js
// array of [key, value] pairs
let map = new Map([
	['1', 'str1'],
	[1, 'num1'],
	[true, 'bool1']
]);

console.log( map.get('1') ); // str1
```

If you already have a plain object and wanting to use this object to create a map, you can use `Object.entries(obj)`:
```js
let obj = {
	name: "Eubug",
	age: 19
};

let map = new Map(Object.entries(obj));

console.log( map.get('name') ); // Eubug
```

Keep in mind that the `Object.entries(obj)` method will convert all keys in the plain object to strings. For instance,

```js
let obj = {
	1: 'one'
};

let map = new Map(Object.entries(obj));

console.log( map.get(1) ); // undefined
console.log( map.get('1') ); // 'one'
```

## Object.fromEntries: Object from Map
We can do the exact opposite of `Object.entries(obj)` where we turn the existing `Map` to an `Object`:

```js
let prices = Object.fromEntries([
	['banana', 1],
	['orange', 2],
	['meat', 4]
]);

// now prices = { banana: 1, orange: 2, meat: 4}
console.log(prices.orange); // 2
```

---

## Set
A `Set` is a special type collection where each value is unique.

### Methods
- `new Set(iterable)` - creates the set. If an `iterable` obj is provided, copies values from it into the set.
- `set.add(value)` - adds a value, returns the set itself.
- `set.delete(value)` - removes the value, returns `true` if `value` existed at the moment of the call, otherwise `false`.
- `set.has(value)` - returns `true` if the value exists in the set, otherwise `false`.
- `set.clear()` - removes everything from the set.
- `set.size` - elements count.

The main feature of `Set` is that repeated calls of `set.add(value)` with the same value don't do anything to the set. That is why each value is unique in the set.

For example, let say you want to log all visitors coming to your party. You don't want to log same person more than once.

So we can use `Set`:
```js
let set = new Set();

let jubug = { name: "Jubug" };
let eubug = { name: "Eubug" };
let mubug = { name: "Mubug" };

// visits
set.add(jubug);
set.add(eubug);
set.add(mubug);
set.add(jubug);
set.add(mubug);

// set keeps only unique values
console.log( set.size ); // 3

for (let user of set) {
	console.log(user.name); // Jubug (then Eubug and Mubug)
}
```

## Iteration over Set
We can use either `for..of` or `forEach` to iterate over `Set`:
```js
let set = new Set(["oranges", "apples", "bananas"]);

for (let value of set) console.log(value);

// the same with forEach:
set.forEach((value, valueAgain, set) => {
	console.log(value);
});
```

Note the three arguments in `set.forEach`. It's a bit strange but this is for compatibility with `Map`. 

The same methods `Map` has for iterators are also supported:
- `set.keys()` - returns an iterable object for values,
- `set.values()` - same as `set.keys()`, for compatibility with `Map`.
- `set.entries()` - returns an iterable for entries `[key, value]`, exists for compatibility with `Map`.

## Reference
- [https://javascript.info/map-set](https://javascript.info/map-set)