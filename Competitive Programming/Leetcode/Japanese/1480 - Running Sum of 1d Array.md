tags: #leetcode #easy #ruby #japanese #array

<hr />

[1480. Running Sum of 1d Array](https://leetcode.com/problems/running-sum-of-1d-array/)

全数のsumを計算した。そして上から逆に数を引いてその値をリストに追加した。

```rb
=begin
 Runtime: 52 ms, faster than 72.86% 
 Memory Usage: 210.1 MB, less than 81.12%
=end
def running_sum(nums)
    sum = nums.sum
    nums << sum;
    
    (nums.size-2).downto(0) do |i|
        temp = nums[i]
        nums[i] = sum - nums[i];
        sum -= temp
    end
    
    nums.shift
    nums
end
```