tags: #leetcode #array #english #cpp #easy

<hr />

[1342. Number of Steps to Reduce a Number to Zero](https://leetcode.com/problems/number-of-steps-to-reduce-a-number-to-zero/)

nothing tricky here. just do as the problem says so.

```cpp
/**
* Runtime: 0 ms, faster than 100.00% 
* Memory Usage: 6.3 MB, less than 31.73%
*/
class Solution {
public:
    int numberOfSteps (int num) {
        int cnt = 0;
        while (num > 0) {
            if (num&1 == 1) --num;
            else num >>= 1;
            
            ++cnt;
        }
        return cnt;
    }
};
```