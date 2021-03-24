tags: #leetcode #math #korean #JavaScript #easy

<hr />

[1281. Subtract the Product and Sum of Digits of an Integer](https://leetcode.com/problems/subtract-the-product-and-sum-of-digits-of-an-integer/)

간단한 수학 문제.

```js
/**
 * Runtime: 80 ms, faster than 48.26% 
 * Memory Usage: 38.4 MB, less than 78.41%
 */
var subtractProductAndSum = function(n) {
  let p = 1;
  let s = 0;

  while (n>0) {
    let t = n%10;
    n = Math.floor(n / 10);

    p *= t;
    s += t;
  }

  return p - s;
};
```

[[Competitive Programming/Leetcode/English/1281 - Subtract the Product and Sum of Digits of an Integer | C++ solution]]
[[Competitive Programming/Leetcode/Japanese/1281 - Subtract the Product and Sum of Digits of an Integer | Ruby solution]]