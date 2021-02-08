tags: #leetcode #easy #cpp #english #array #bit-manipulation 

<hr />

[1486. XOR Operation in an Array](https://leetcode.com/problems/xor-operation-in-an-array/)

```cpp
/**
 * Runtime: 0 ms, faster than 100.00%
 * Memory Usage: 6.1 MB
 */
class Solution {
  public:
    int xorOperation(int n, int start) {
      int result = start;
      for(int i=1; i<n; ++i) 
      {
        result = result ^ (start + 2*i);
      }

      return result;
    }
};
```

[[Competitive Programming/Leetcode/Korean/1486 - XOR Operation in an Array | JavaScript solution]]
[[Competitive Programming/Leetcode/Japanese/1486 - XOR Operation in an Array | Ruby solution]]