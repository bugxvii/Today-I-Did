tags: #leetcode #array #korean #JavaScript #easy

<hr />

[1389. Create Target Array in the Given Order](https://leetcode.com/problems/create-target-array-in-the-given-order/)

주어진 index순으로 요소들을 리스트에 삽입하면 된다.

```js
/**
 * Runtime: 80 ms, faster than 47.00%
 * Memory Usage: 38.9 MB, less than 23.33%
 */
var createTargetArray = function(nums, index) {
  let result = []
  for(let i=0; i<index.length; ++i) {
    result.splice(index[i], 0, nums[i]);
  }

  return result;
};
```

[[Competitive Programming/Leetcode/English/1389 - Create Target Array in the Given Order | C++ solution]]
[[Competitive Programming/Leetcode/Japanese/1389 - Create Target Array in the Given Order | Ruby solution]]