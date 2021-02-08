tags: #leetcode #array #english #cpp #easy

<hr />

[1431. Kids With the Greatest Number of Candies](https://leetcode.com/problems/kids-with-the-greatest-number-of-candies/)

first find the max and use that value to create a boolean list.

```cpp
/*
 * Runtime: 4 ms
 * Faster than 81.66%
 * Memory Usage: 9.3 MB, less than 100%
 * */

class Solution {
public:
    vector<bool> kidsWithCandies(vector<int>& candies, int extraCandies) {
        vector<bool> result;
        int _max = -1;
        for(int i=0; i<candies.size(); ++i)
            if (candies[i] > _max) _max = candies[i];

        for(int i=0; i<candies.size(); ++i)
            if (candies[i] + extraCandies >= _max) result.push_back(true);
            else result.push_back(false);

        return result;
    }
};
```