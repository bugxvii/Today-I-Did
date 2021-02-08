tags: #leetcode #array #english #cpp #easy

<hr />

[1389. Create Target Array in the Given Order](https://leetcode.com/problems/create-target-array-in-the-given-order/)

simply insert the number in a given array.

```cpp
/**
 * Runtime: 0 ms, faster than 100.00%
 * Memory Usage: 8.8 MB, less than 34.60%
 */
class Solution {
  public:
    vector<int> createTargetArray(vector<int>& nums, vector<int>& index) {
      vector<int> result;

      for (int i=0; i<index.size(); ++i)
      {
        auto it = result.begin();
        result.insert(it + index[i], nums[i]);
      }


      return result;
    }
};
```

[[Competitive Programming/Leetcode/Korean/1389 - Create Target Array in the Given Order | JavaScript solution]]
[[Competitive Programming/Leetcode/Japanese/1389 - Create Target Array in the Given Order | Ruby solution]]