tags: #leetcode #array #hash-table #korean #JavaScript #easy

<hr />

[1365. How Many Numbers Are Smaller Than the Current Number](https://leetcode.com/problems/how-many-numbers-are-smaller-than-the-current-number/) 

```js
/**
 * Runtime: 96 ms, faster than 68.18%
 * Memory Usage: 41 MB, less than 13.65%
 */
var smallerNumbersThanCurrent = function(nums) {
  let temp = [...nums];
  temp = temp.sort((a, b) => {return a-b;});
  let table = new Array(101).fill(0);
  let cnt = 1;
  table[nums[0]] = 0;
  for(let i=1; i<nums.length; ++i) {
    table[temp[i]] = ((temp[i-1] == temp[i]) ? table[temp[i-1]] : cnt);
    ++cnt;
  }

  for(let i=0; i<nums.length; ++i) {
    temp[i] = table[nums[i]];
  }

  return temp;
};
```

[[Competitive Programming/Leetcode/English/1365 - How Many Numbers Are Smaller Than the Current Number | C++ solution]]
[[Competitive Programming/Leetcode/Japanese/1365 - How Many Numbers Are Smaller Than the Current Number | Ruby solution]]