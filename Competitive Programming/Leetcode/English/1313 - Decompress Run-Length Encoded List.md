tags: #leetcode #array #english #cpp #easy

<hr />

[1313. Decompress Run-Length Encoded List](https://leetcode.com/problems/decompress-run-length-encoded-list/)

read two numbers at a time and re-create the list.

```cpp
/*
 * Runtime: 4 ms, faster than 95.70% 
 * Memory Usage: 10.2 MB, less than 83.96%
 */
class Solution {
  public:
    vector<int> decompressRLElist(vector<int>& nums) {
      vector<int> result;
      for(int i=0; i<nums.size(); i+=2) 
      {
        int freq = nums[i];
        int val = nums[i+1];

        for(int j=0; j<freq; ++j)
        {
          result.push_back(val);
        }
      }
      return result;
    }
};
```

[[Competitive Programming/Leetcode/Korean/1313 - Decompress Run-Length Encoded List | JavaScript solution]]
[[Competitive Programming/Leetcode/Japanese/1313 - Decompress Run-Length Encoded List | Ruby solution]]