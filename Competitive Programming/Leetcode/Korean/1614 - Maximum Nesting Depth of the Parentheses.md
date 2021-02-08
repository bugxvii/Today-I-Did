tags: #leetcode #easy #JavaScript #korean #string

<hr />

[1614. Maximum Nesting Depth of the Parentheses](https://leetcode.com/problems/maximum-nesting-depth-of-the-parentheses/)

간단한 카운팅.

```js
/**
 * Runtime: 88 ms, faster than 23.24%
 * Memory Usage: 38.4 MB, less than 92.83%
 */
var maxDepth = function(s) {
  let cnt = 0
  let max = 0

  for (let i=0; i<s.length; ++i) {
    if (s[i] == '(') ++cnt;
    else if(s[i] == ')') --cnt;

    max = (cnt > max) ? cnt : max;
  }

  return max;
};
```

[[Competitive Programming/Leetcode/English/1614 - Maximum Nesting Depth of the Parentheses | C++ solution]]
[[Competitive Programming/Leetcode/Japanese/1614 - Maximum Nesting Depth of the Parentheses | Ruby solution]]