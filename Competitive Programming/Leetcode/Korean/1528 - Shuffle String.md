tags: #leetcode #easy #JavaScript #korean #sort

<hr />

[1528. Shuffle String](https://leetcode.com/problems/shuffle-string/)

```js
/**
 * Runtime: 88 ms, faster than 73.88%
 * Memory Usage: 39.2 MB, less than 79.04%
 */
var restoreString = function(s, indices) {
    let result = new Array(indices.length);
    let j = 0;
    indices.forEach(i => {
        result[i] = s[j];
        j+=1
    })
    
    return result.join('');
};
```

[[Competitive Programming/Leetcode/English/1528 - Shuffle String | C++ solution]]
[[Competitive Programming/Leetcode/Japanese/1528 - Shuffle String | Ruby solution]]