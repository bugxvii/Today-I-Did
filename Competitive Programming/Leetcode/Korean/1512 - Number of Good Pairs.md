tags: #leetcode #easy #korean #JavaScript #array #hash-table #math

<hr />

[1512. Number of Good Pairs](https://leetcode.com/problems/number-of-good-pairs/)

주어진 조건을 따라서 브루트포스 방법으로 하나하나 찾았다.

```js
/**
 * Runtime: 80 ms, faster than 47.12%.
 * Memory Usage: 38.4 MB, less than 56.81%.
 */
var numIdenticalPairs = function(nums) {
    let cnt = 0;
    for(let i=0; i<nums.length; ++i) {
        for(let j=i+1; j<nums.length; ++j) {
            if (nums[i] == nums[j]) ++cnt;
        }
    }
    return cnt;
};
```

[[Competitive Programming/Leetcode/English/1512 - Number of Good Pairs | C++ solution]]
[[Competitive Programming/Leetcode/Japanese/1512 - Number of Good Pairs | Ruby solution]]