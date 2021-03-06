tags: #JavaScript #regex #english

---

What is **Regular Expression**?

Regular Expressions, *Regex*, are patterns used to match characters combinations in strings. In JavaScript, regex are objects.

They are used with `exec()` and `test()` methods in `RegExp`. And `match()`, `matchAll()`, `replace()`, `replaceAll()`, and `split()` methods of `String`.

## Creating a regular expression
There are two ways to construct a regex:
1. Use a regex literal which consists of a pattern enclosed between slashes:
```js
let re = /ab+c/;
```
If you know that the regex will remain constant, using the literal can improve the performance.

2. Call the constructor function of the `RegExp` object:
```js
let re = new RegExp('ab+c');
```
Use the constructor way if your regex is changing, or you don't know the pattern and getting it from the user input (or other source).

## Using Simple Patterns
Simple patterns like `/abc/` matches character combinations in strings only when the exact sequence *'abc'* occurs.

So `/abc/` will match with strings like *"abcdef"* or *"Hi, do you know your abc's?"*. But won't match with the string *"Grab crab"* because "ab c" is not a direct match with "abc".

## Using Special Characters
To match a string that is more than just a direct match like *"abbc"* or *"abbbbbbc"*, we can use a special character in the pattern.

For example, to match a single `'a'` *followed by one or more* `'b'`s *followed by* `'c'`, we can use the pattern `/ab+c/`.

This `+` after a `'b'` means *one or more*. If you want *any number of `'b'` including zero*, you can use `/ab*c/`.

- `/ab*c/` - zero or more `'b'`
- `/ab+c/` - one or more `'b'`

## Escaping
To match characters like `'*'` in the string, we need to escape it using the backslash in front of it:
```js
// match a string that has 0 or more '*' in betwwen "AB"
let re = /A\**B/;
```

## Using Regex in JavaScript
### RegExp
- `exec()`: executes a search for a match in a string. It returns an array of information or *null* on a mismatch.
- `test()`: test for a match in a string. It returns `true` or `false`.

```js
let re = /ab*c/g;

re.exec("ac abc abbc"); // ac
re.exec("ac abc abbc"); // abc
re.exec("ac abc abbc"); // abbc
re.exec("ac abc abbc"); // null

re.test("ac abc abbc"); // true
re.test("ac abc abbc"); // true
re.test("ac abc abbc"); // true
re.test("ac abc abbc"); // false
```

### String
- `match()`: returns an array containing all of the matches, including capturing groups, or *null* if no match is found.
- `matchAll()`: returns an iterator containing all of the matches, including capturing groups.
- `search()`: test for a match in a string. It returns the index of the match or *-1* if the search fails.
- `replace()`: replaces the matched substring with a replacement substring.
- `replaceAll()`: replaces all matched substrings with a replacement substring.
- `split()`: uses a regex or a fixed string to break a string into an array of substrings.

## Tools
- [Regexer](https://regexr.com)
- [Regex Visualizer](https://extendsclass.com/regex-tester.html#js)

## Reference
- [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)