tags: #leetcode #math #english #cpp #easy

<hr />

[1281. Subtract the Product and Sum of Digits of an Integer](https://leetcode.com/problems/subtract-the-product-and-sum-of-digits-of-an-integer/)

simple math problem. do as the problem says.

```cpp
/*
 * Runtime: 0 ms, faster than 100.00%
 * Memory Usage: 6.2 MB, less than 64.71%
 */
class Solution {
  public:
    int subtractProductAndSum(int n) {
      int p = 1;
      int s = 0;

      while(n>0) 
      {
        int t = n%10;
        n = n/10;

        p *= t;
        s += t;
      }

      return p - s;
    }
};
```

[[Competitive Programming/Leetcode/Korean/1281 - Subtract the Product and Sum of Digits of an Integer | JavaScript solution]]
[[Competitive Programming/Leetcode/Japanese/1281 - Subtract the Product and Sum of Digits of an Integer | Ruby solution]]