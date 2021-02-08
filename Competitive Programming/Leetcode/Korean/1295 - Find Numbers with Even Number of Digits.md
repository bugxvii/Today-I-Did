tags: #leetcode #array #korean #JavaScript #easy

<hr />

[1295. Find Numbers with Even Number of Digits](https://leetcode.com/problems/find-numbers-with-even-number-of-digits/)

숫자를 문자열로 변환한 다음 길이를 확인했다.

```js
/**
 * Runtime: 80 ms, faster than 75.32%
 * Memory Usage: 39.1 MB, less than 77.61%
 */
var findNumbers = function(nums) {
  let result = 0;

  nums.forEach(e => {
    if (e.toString().length % 2 == 0) ++result;
  });

  return result;
};
```

[[Competitive Programming/Leetcode/English/1295 - Find Numbers with Even Number of Digits | C++ solution]]
[[Competitive Programming/Leetcode/Japanese/1295 - Find Numbers with Even Number of Digits | Ruby solution]]