tags: #leetcode #string #korean #JavaScript  #easy

<hr />

[1108. Defanging an IP Address](https://leetcode.com/problems/defanging-an-ip-address/)

문자를 한 번에 치환하거나 따로따로 _\[.\]_ 를 추가하면 된다.

```js
/**
 * Runtime: 68 ms, faster than 95.34%
 * Memory Usage: 38.6 MB, less than 24.72%
 */
var defangIPaddr = function(address) {
    const regex = /\./gi;
    return address.replace(regex, '[.]');
};
```

[[Competitive Programming/Leetcode/English/1108 - Defanging an IP Address | C++ solution]]
[[Competitive Programming/Leetcode/Japanese/1108 - Defanging an IP Address | Ruby solution]]