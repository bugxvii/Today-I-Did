tags: #leetcode #easy #cpp #english #array

<hr />

[1672. Richest Customer Wealth](https://leetcode.com/problems/richest-customer-wealth/)

bruteforce (i think?)

```cpp
/*
 * Runtime: 12 ms, faster than 39.22% 
 * Memory Usage: 8.1 MB, less than 60.83%
 */
class Solution {
  public:
    int maximumWealth(vector<vector<int>>& accounts) {
      int max = -1;
      for(int i=0; i<accounts.size(); ++i) {
        int sum = 0;
        for(int j=0; j<accounts[i].size(); ++j) {
          sum += accounts[i][j];
        }
        max = sum > max ? sum : max;
      }
      return max;
    }
};
```

[[Competitive Programming/Leetcode/Korean/1672 - Richest Customer Wealth | JavaScript solution]]
[[Competitive Programming/Leetcode/Japanese/1672 - Richest Customer Wealth | Ruby solution]]