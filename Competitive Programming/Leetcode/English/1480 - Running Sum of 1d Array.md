tags: #leetcode #easy #cpp #english #array

<hr />

[1480. Running Sum of 1d Array](https://leetcode.com/problems/running-sum-of-1d-array/)

i first found the sum of all numbers and work my way down reversely.

```cpp
/*
 * Runtime: 12 ms, faster than 13.10% 
 * Memory Usage: 8.9 MB, less than 98.70%
 */
class Solution {
public:
    vector<int> runningSum(vector<int>& nums) {
        vector<int> result;
        for(int i=0; i<nums.size(); ++i)
        {
            int sum = 0;
            for(int j=0; j<i+1; ++j)
            {
                sum += nums[j];
            }
            result.push_back(sum);
        }
        return result;
    }
};

/*
 * Runtime: 4 ms, faster than 84.50% 
 * Memory Usage: 8.9 MB, less than 98.70%
*/
class Solution {
public:
    vector<int> runningSum(vector<int>& nums) {
        int sum = 0;
        for(int i=0; i<nums.size(); ++i)
        {
            sum += nums[i];
        }
        
        int neg = nums[nums.size()-1];
        nums[nums.size()-1] = sum;
        for (int i=nums.size()-2; i>=0; --i)
        {
            int val = sum-neg;
            neg += nums[i];
            nums[i] = val;
        }
        return nums;
    }
};
```

[[Competitive Programming/Leetcode/Korean/1480 - Running Sum of 1d Array | JavaScript solution]]
[[Competitive Programming/Leetcode/Japanese/1480 - Running Sum of 1d Array | Ruby solution]]