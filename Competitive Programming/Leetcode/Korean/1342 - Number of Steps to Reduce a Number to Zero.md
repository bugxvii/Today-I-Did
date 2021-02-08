tags: #leetcode #array #korean #JavaScript #easy

<hr />

[1342. Number of Steps to Reduce a Number to Zero](https://leetcode.com/problems/number-of-steps-to-reduce-a-number-to-zero/)

문제에서 시키는 대로 하자.

```js
/**
 * Runtime: 80 ms, faster than 65.29%
 * Memory Usage: 38.8 MB, less than 26.72% 
 */
var numberOfSteps  = function(num) {
    let cnt = 0;
    
    while (num > 0) {
        if ((num & 1) == 0) num = num / 2;
        else num -= 1;
        ++cnt;
    }
    
    return cnt;
};
```

[[Competitive Programming/Leetcode/English/1342 - Number of Steps to Reduce a Number to Zero | C++ solution]]
[[Competitive Programming/Leetcode/Japanese/1342 - Number of Steps to Reduce a Number to Zero | Ruby solution]]