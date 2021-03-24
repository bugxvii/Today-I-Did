tags: #leetcode #easy #JavaScript #korean #string

<hr />

[1662. Check If Two String Arrays are Equivalent](https://leetcode.com/problems/check-if-two-string-arrays-are-equivalent/)
    
글자 하나하나 반복문으로 비교하면 된다.

```js
/**
 * Runtime: 84 ms, faster than 100.00%
 * Memory Usage: 38.8 MB, less than 100.00%
 */
var arrayStringsAreEqual = function(word1, word2) {
  let str1 = word1.join('');
  let str2 = word2.join('');

  if (str1.length != str2.length) {
    return false;
  }

  for (let i=0; i<str1.length; ++i) {
    if (str1[i] != str2[i])
      return false;
  }

  return true;
};
```

[[Competitive Programming/Leetcode/English/1662 - Check If Two String Arrays are Equivalent | C++ solution]]
[[Competitive Programming/Leetcode/Japanese/1662 - Check If Two String Arrays are Equivalent | Ruby solution]]