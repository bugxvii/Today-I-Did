tags: #leetcode #hash-table #korean #JavaScript #easy

<hr />

[771. Jewels and Stones](https://leetcode.com/problems/jewels-and-stones/)

```js
/**
 * Runtime: 80 ms, faster than 79.03%
 * Memory Usage: 38.8 MB, less than 62.63%
 */
var numJewelsInStones = function(J, S) {
    let cnt = 0;
    S = S.split('');
    S.forEach(c => {
        (J.includes(c)) ? cnt += 1 : cnt;
    })
    
    return cnt;
};
```

[[Competitive Programming/Leetcode/English/771 - Jewels and Stones | C++ solution]]
[[Competitive Programming/Leetcode/Japanese/771 - Jewels and Stones | Ruby solution]]