tags: #leetcode #array #hash-table #japanese #ruby #easy

<hr />

[1365. How Many Numbers Are Smaller Than the Current Number](https://leetcode.com/problems/how-many-numbers-are-smaller-than-the-current-number/) 

```rb
# Runtime: 72 ms, faster than 74.00%
# Memory Usage: 210.5 MB, less than 45.00%
def smaller_numbers_than_current(nums)
  temp = nums.sort;
  table = [0]*101;

  cnt = 1
  1.upto(temp.size-1) do |i|
    table[temp[i]] = ((temp[i-1] == temp[i]) ? table[temp[i-1]] : cnt)
    cnt += 1
  end

  0.upto(nums.size - 1) do |i|
    temp[i] = table[nums[i]]
  end

  temp
end
```