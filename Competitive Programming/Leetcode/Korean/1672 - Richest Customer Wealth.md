tags: #leetcode #easy #JavaScript #korean #array

<hr />

[1672. Richest Customer Wealth](https://leetcode.com/problems/richest-customer-wealth/)

브루트포스 같은데 생각보다 실행 시간이 느리다. 어떻게 빨리 돌리지?

```js
/**
 * Runtime: 80 ms, faster than 56.45% 
 * Memory Usage: 38.7 MB, less than 35.23%
 */
var maximumWealth = function(accounts) {
  let max = 0;
  accounts.forEach((bank) => {
    let sum = 0;
    bank.forEach((money) => {
      sum += money;
    });
    max = sum > max ? sum : max;
  });

  return max;
};
```

[[Competitive Programming/Leetcode/English/1672 - Richest Customer Wealth | C++ solution]]
[[Competitive Programming/Leetcode/Japanese/1672 - Richest Customer Wealth | Ruby Solution]]