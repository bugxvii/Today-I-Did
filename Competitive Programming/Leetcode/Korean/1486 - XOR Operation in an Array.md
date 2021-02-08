tags: #leetcode #easy #JavaScript #korean #array #bit-manipulation 

<hr />

[1486. XOR Operation in an Array](https://leetcode.com/problems/xor-operation-in-an-array/)

```js
/**
 * Runtime: 60 ms, faster than 100.00%
 * Memory Usage: 38.2 MB, less than 83.71%
 */
var xorOperation = function(n, start) {
  let result = start;

  for (let i=1; i<n; ++i) {
    result = result ^ (start + 2*i);
  }

  return result;
};
```

[[Competitive Programming/Leetcode/English/1486 - XOR Operation in an Array | C++ solution]]
[[Competitive Programming/Leetcode/Japanese/1486 - XOR Operation in an Array | Ruby solution]]