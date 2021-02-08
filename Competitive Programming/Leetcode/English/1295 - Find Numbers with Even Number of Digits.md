tags: #leetcode #array #english #cpp #easy

<hr />

[1295. Find Numbers with Even Number of Digits](https://leetcode.com/problems/find-numbers-with-even-number-of-digits/)

not the best way but i just divided given number by 10 until it reaches 0 and checked whether this number has even number of digits.

```cpp
/**
 * Runtime: 12 ms, faster than 38.52%
 * Memory Usage: 10.2 MB, less than 53.11%
 */
class Solution {
  public:
    int findNumbers(vector<int>& nums) {
      int result = 0;

      for(int x : nums) 
      {
        int cnt = 0;
        while (x>0) {
          ++cnt;
          x /= 10;
        }

        result = (cnt & 1) ? result : result + 1;
      }

      return result;
    }
};
```