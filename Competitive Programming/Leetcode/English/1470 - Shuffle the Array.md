tags: #leetcode #array #english #cpp #easy

<hr />

[1470. Shuffle the Array](https://leetcode.com/problems/shuffle-the-array/)

```cpp
/*
 * Runtime: 8 ms, faster than 89.28% of C++ online submissions for Shuffle the Array.
 * Memory Usage: 10.3 MB, less than 100.00% of C++ online submissions for Shuffle the Array.
*/

class Solution {
public:
    vector<int> shuffle(vector<int>& nums, int n) {
        vector<int> result;
        
        for (int i=0; i<n; ++i)
        {
            result.push_back(nums[i]);
            result.push_back(nums[n+i]);
        }
        
        return result;
    }
};
```