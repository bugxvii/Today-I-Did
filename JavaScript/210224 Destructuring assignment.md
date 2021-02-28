tags: #JavaScript #data-type #modern-js #english

---

The two most used data structures in JS are `Object` and `Array`.

- Objects allow us to create a single entity that stores data items by key.
- Arrays allow us to gather data items into an ordered list.

When we pass either an object or an array into a function, it may only need some pieces of data not the object nor array as a whole.

*Destructuring assignment* is a special syntax that allows us to "unpack" arrays or objects into a bunch of variables.

## Array destructuring
```js
// we have an array with the name and surname
let arr = ["John", "Smith"]

// destructuring assignment
// sets firstName = arr[0]
// and surname = arr[1]
let [firstName, surname] = arr;

console.log( firstName ); // John
console.log( surname ); // Smith
```

We can also use `split()` or other array-returning methods:
```js
let [firstName, surname] = "John Smith".split(' ');
console.log( firstName ); // John
console.log( surname ); // Smith
```

### The rest '...'
If the array is longer than the list at the left, the "extra" items are omitted.

```js
let [name1, name2] = ["Julius", "Caesar", "Consul", "of the Roman Republic"];

console.log( name1 ); // Julius
console.log( name2 ); //  Caesar
// further items aren't assigned anywhere
```

We can use three dots (`...`) which means *"the rest"*:
```js
let [name1, name2, ...rest] = ["Julius", "Caesar", "Consul", "of the Roman Republic"];

// rest is array of items
console.log( rest[0] ); // Consul
console.log( rest[1] ); // of the Roman Republic
console.log( rest.length ); // 2
```

The value of the `rest` is the remaining array elements.

### Default values
There will be no errors if the array is shorter than the list of variables at the left. Absent values are considered undefined:
```js
let [firstName, surname] = [];

console.log( firstName ); // undefined
console.log( surname ); // undefined
```

We can set the default value:
```js
// default values
let [name = "Guest", surname = "Anonymous"] = ["Julius"];

console.log( name ); // Julius (from array)
console.log( surname ); // 'Anonymous' is a wrong password.
```

## Object destructuring
The basic syntax:
```js
let {var1, var2} = {var1:..., var2:...}
```

Let's take a look at the example:
```js
let options = {
	title: "Menu",
	width: 100,
	height: 200
};

let {title, width, height} = options;

console.log( title ); // Mnu
console.log( width ); // 120
console.log( height ); // 200
```

> orders on the left side does not mater.

### Changing the property name
If you want to assign a property to a variable with another name:
```js
let options = {
	title: "Menu",
	width: 100,
	height: 200
};

// { sourceProperty: targetVariable }
let {width: w, height: h, title} = options;

// width -> w
// height -> h
// title -> title

console.log( title ); // Menu
console.log( w ); // 100
console.log( h ); // 200
```

### Default values
Just like Objects, we can set default values using "=":

```js
let options = {
	titl: "Menu"
};

let {width = 100, height = 200, title} = options;

console.log( title ); // Menu
console.log( width ); // 100
console.log( height ); // 200
```

### Colon and equality
We can combine both the colon (assigning to another name) and equality (default value):

```js
let options = {
	title: "Menu"
};

let { width: w = 100, height: h = 200, title } = options;

console.log( title ); // Menu
console.log( w ); // 100
console.log( h ); // 200
```

### Extract
We can only extract properties that we're going to use:
```js
let options = {
	title: "Menu",
	width: 100,
	height: 200
};

let { title } = options;

console.log( title ); // Menu
```

### The  rest pattern "..."
Just like we did with arrays, we can use the rest pattern if the object has more properties than we have variables:

```js
let options = {
	title: "Menu",
	height: 200,
	width: 100
};

// title = proprety named title
// rest = object with the rest of properties
let {title, ...rest} = options;

// now title="Menu", rest={height: 200, width: 100}
console.log( rest.height ); // 200
console.log( rest.width ); // 100
```

## Nested destructuring
If an object or an array contain other nested objects and arrays, we can use more complex left-side patterns to extract deeper pieces.

```js
let optinos = {
	size: {
		width: 100,
		height: 200
	},
	items: ["Cake", "Donut"],
	extra: true
};

// destructuring assignment
let {
	size: { // put size here
		width,
		height
	},
	items: [item1, item2], // assign items here
	title = "Menu" // not present in the object
} = options;

console.log( title ); // Menu
console.log( width ); // 100
console.log( height ); // 100
console.log( item1 ); // Cake
console.log( item2 ); // Donut
```

## Reference
- [https://javascript.info/destructuring-assignment](https://javascript.info/destructuring-assignment)

minsunny5@gmail.com
안녕하세요. 반갑습니다. 유버그입니다. 기초 알고리즘 & 자료구조 스터디 용 디스코드 채널을 만들었습니다. [https://discord.gg/PmT8TzTG](https://t.co/uMruLOJoVz?amp=1) 입장 후, 아이디는 트위터 아이디랑 동일시해주세요. 깃허브 리포는 후에 만들고 다시 연락드리겠습니다.

스터디는 처음이라 미숙할테지만, 잘 부탁드립니다.