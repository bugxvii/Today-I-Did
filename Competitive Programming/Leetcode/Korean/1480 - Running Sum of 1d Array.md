tags: #leetcode #easy #JavaScript #korean #array

<hr />

[1480. Running Sum of 1d Array](https://leetcode.com/problems/running-sum-of-1d-array/)

모든 숫자들의 합을 먼저 구한 다음 거꾸로 내려오면서 풀었다.

```js
/**
 * Runtime: 80 ms, faster than 66.97%
 * Memory Usage: 38.7 MB, less than 5.17%
 */
var runningSum = function(nums) {
    let sum = nums.reduce((a, b) => a + b, 0);
    let neg = nums[nums.length-1];
    nums[nums.length-1] = sum;
    
    for (let i=nums.length-2; i>=0; --i) {
        let val = sum - neg;
        neg += nums[i];
        nums[i] = val;
    }
    
    return nums;
};
```

[[Competitive Programming/Leetcode/English/1480 - Running Sum of 1d Array | C++ solution]]
[[Competitive Programming/Leetcode/Japanese/1480 - Running Sum of 1d Array | Ruby solution]]