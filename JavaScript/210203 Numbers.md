tags: #JavaScript #data-type 

<hr />

## Numbers 
There are two types of numbers in modern JavaScript:
1. Regular numbers - [IEEE-754](https://en.wikipedia.org/wiki/IEEE_754-2008_revision) (double precision floating point numbers)
2. [BigInt](https://javascript.info/bigint) numbers.

## Ways to write numbers
Here's how people normally define numbers
```js
let billion = 1000000000;
```

### separators
We can use underscore(`_`) as the separator:
```js
let billion = 1_000_000_000;
```

### scientific notation
We can use `"e"` to represent a [scientific notation](https://www.mathsisfun.com/numbers/scientific-notation.html).
```js
let billion = 1e9;    // 1 billion
console.log( 7.3e9 ); // 7.3 billions
```

We use `"e"` not only to represent big numbers, but also very small numbers.
```js
let ms = 1e-6; // six zeroes to the left from 1 -> 0.000001;
```

## Hex, binary and octal
The modern JavaScript supports three different numeral systems: hexadecimal, binary and octal; that is base 16, 2, and 8, respectively. 

If you want to use other numeral systems such as base 3 or base 7, please use `parseInt` function.

### hexadecimal
We represent [hexadecimal](https://en.wikipedia.org/wiki/Hexadecimal) numbers with the `0x` prefix.

For instance:
```js
console.log( 0xff ); // 255
console.log( 0xFF ); // 255 (same, case insensitive)
```

- Used for hex colors,
- character encodings
- digits can be `0..9` or `A..F`.

### binary
We can define binary numbers with the `0b` prefix.

```js
let a = 0b11111111; // binary form of 255
```

- Used mostly for debugging bitwise operations.

### octal
Octal (base 8) number systems are also supported by the language. If you write a number with the `0o` prefix, the number will be considered to be in octal format.

```js
let b = 0o377; // octal form of 255
```

## toString(base)
The method `num.toString(base)` returns a string representation of `num` in the numeral system with the given `base`.

```js
let num = 255;

console.log( num.toString(16) ); // ff
console.log( num.toString(2) ); // 11111111;
```

The base can vary from `2` to `36`. By default, it is `10`

## Rounding
- `Math.floor`: Rounds down
.	==> 3.1 -> 3 and -1.1 -> -2
- `Math.ceil`: Rounds  up.
	==> 3.1 -> 4 and -1.1 -> -1
- `Math.round`: Rounds to the nearest integer...
	==> 3.1 -> 3 and 3.6 -> 4
- `Math.trunc` (not supported by IE) -> Removes anything after the decimal point without rounding.
	==> 3.1 -> 3.0 and 3.6 -> 4.0

### Round numbers to N-th digit 
We can round numbers to a whole number, but what if we want to round numbers to certain number of digits?

For instance, we want to round `1.2345` to `1.23`. There are several ways to accomplish this.

1. Multiply-and-divide
	```js
	let num = 1.2345;
	
	// 1.12345 -> 123.456 -> 123 -> 1.23
	console.log( num.floor(num * 100) / 100 ) );
	```
2. `toFixed(n)` - rounds the number to `n` digits after the point and returns a string representation of the result.
	```js
	let num = 1.2345;
	
	console.log( num.toFixed(1) ); // 1.2
	```

Note that if the decimal part is shorter than required, zeroes are appended to the end:
```js
let num = 1.234;
console.log ( num.toFixed(5) ); // 1.23400
```

## Imprecise calculations
As we mentioned earlier, JavaScript has two types of numbers and **[IEEE-754](https://en.wikipedia.org/wiki/IEEE_754-2008_revision)** is one of  them.

IEEE-754 uses 64-bit format. 
- 52 bits to store digits (fractions)
- 11 bits to store the position of the decimal point (exponents)
- 1 bit for the sign

When numbers are too big, it will overflow 64-bits storage and result in infinity:
```js
console.log( 1e500 ); // Infinity
```

However, when performing arithmetic operations with small numbers, the result is not quite obvious.
```js
console.log( 0.1 + 0.2 == 0.3 ); // false
```

The result is `false`. This is not so easy to understand at a glance without understanding the loss of precision.

So what is `0.1 + 0.2`? 

Here it is.

```js
console.log ( 0.1 + 0.2 ); // 0.30000000000000004
```

A number is stored in memory in its binary form. But fractions like `0.1` and `0.2` are actually unending fractions in their binary form. Similary to `0.3333...`, there's no way to store **exactly** `0.1` or `0.2` using the binary system, just like there's no way to store `0.3333...` as a decimal fraction.

IEEE-754 solves this by rounding to the nearest possible number. These rounding rules normally don't allow us to see that *tiny precision loss* but it exists. 

```js
console.log( 0.1.toFixed(20) ); // "0.10000000000000000555"
```

And that is why `0.1 + 0.2` is **not exactly** `0.3`.

### work around
So to correctly add and display `0.1 + 0.2`, we can 
1. round the result with `toFixed(n)`
	```js
	let sum = 0.1 + 0.2;
	console.log( +sum.toFixed(2) ); // 0.3
	```
2. Multiply by 100 (or a bigger number).
	```js
	let sum = (0.1 * 10) + (0.2 * 10) / 10;
	console.log( sum ); // 0.3
	```
	
## parseInt and parseFloat
We can convert a string to numbers using `+` or `Number()`. But there are limitations. 

For instance:

```js
console.log( +"100px" ); // NaN
```

So if a number is not exactly a number, it will return `NaN`. To get numbers from a string like `"100px"` or `"12pt"`, we use `parseInt` for integers and `parseFloat` for floating point numbers.

```js
console.log( parseInt('100px') ); // 100
console.log( parseFloat('12.5em') ); // 12.5

console.log( parseInt('12.3') ); // 12
console.log( parseFloat('12.3.4') ); // 12.3
```

`parse` method simply reads a number digit by digit until it is not a number. So when you have a string like `a123`, it fails to read any number so it will return `NaN`.

The `parseInt` function has an optional second parameter which you can use to specify the base of the numeral system.

```js
console.log( parseInt('0xff', 16) ); // 255
console.log( parseInt('ff', 16) ); // 255, without 0x also works

console.log( parseInt('2n9c', 36) );  // 123456
```

## Other math functions
JavaScript has a built-in [Math](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math) object which contains a small library of mathematical functions and constants.

## Reference
- https://javascript.info/number