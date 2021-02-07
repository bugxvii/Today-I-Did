tags: #leetcode #array #japanese #ruby #easy

<hr />

[1470. Shuffle the Array](https://leetcode.com/problems/shuffle-the-array/)

```rb
# Runtime: 48 ms, faster than 89.60% of Ruby online submissions for Shuffle the Array.
# Memory Usage: 210.7 MB, less than 61.85% 

def shuffle(nums, n)
    result = []
    
    1.upto(n) do |i|
        result << nums[i-1];
        result << nums[n+(i-1)]
    end
    result
end
```