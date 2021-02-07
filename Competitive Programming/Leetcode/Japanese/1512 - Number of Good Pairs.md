tags: #leetcode #easy #ruby #japanese #array #hash-table #math

<hr />

[1512. Number of Good Pairs](https://leetcode.com/problems/number-of-good-pairs/)

ブルートフォース。

```rb
# Runtime: 48 ms, faster than 79.58%
# Memory Usage: 209.7 MB, less than 70.42%
def num_identical_pairs(nums)
    cnt = 0
    0.upto(nums.size-1) do |i|
        (i+1).upto(nums.size-1) do |j|
            if nums[i] == nums[j]
                cnt += 1                
            end
        end
    end
    cnt
end
```