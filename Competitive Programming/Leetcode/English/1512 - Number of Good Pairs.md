tags: #leetcode #easy #english #cpp #array #hash-table #math

<hr />

[1512. Number of Good Pairs](https://leetcode.com/problems/number-of-good-pairs/)

bruteforce.

```cpp
/**
* Runtime: 4 ms, faster than 54.71%
* Memory Usage: 7.5 MB, less than 56.34%
*/
class Solution {
public:
    int numIdenticalPairs(vector<int>& nums) {
        int cnt = 0;
        for (int i=0; i<nums.size(); ++i)
        {
            for (int j=i+1; j<nums.size(); ++j)
            {
                if (nums[i] == nums[j]) ++cnt;
            }
        }
        
        return cnt;
    }
};
```

[[Competitive Programming/Leetcode/Korean/1512 - Number of Good Pairs | JavaScript solution]]
[[Competitive Programming/Leetcode/Japanese/1512 - Number of Good Pairs | Ruby solution]]