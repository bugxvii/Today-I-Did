tags: #leetcode #array #korean #JavaScript #easy

<hr />

[1313. Decompress Run-Length Encoded List](https://leetcode.com/problems/decompress-run-length-encoded-list/)

리스트에서 두 숫자씩 읽으면서 새로운 리스트를 만들어나간다.

```js
/**
 * Runtime: 100 ms, faster than 50.06%
 * Memory Usage: 42.2 MB, less than 66.48%
 */
var decompressRLElist = function(nums) {
  let result = []

  for (let i=0; i<nums.length; i+=2) {
    let f = nums[i];
    let v = nums[i+1];

    for (let j=0; j<f; ++j) {
      result.push(v);
    }
  }

  return result;
};
```

[[Competitive Programming/Leetcode/English/1313 - Decompress Run-Length Encoded List | C++ solution]]
[[Competitive Programming/Leetcode/Japanese/1313 - Decompress Run-Length Encoded List | Ruby solution]]