tags: #leetcode #array #japanese #ruby #easy

<hr />

[1389. Create Target Array in the Given Order](https://leetcode.com/problems/create-target-array-in-the-given-order/)

与えれたindexの順番に要素をリストに入れる。

```rb
# Runtime: 40 ms, faster than 90.00% 
# Memory Usage: 210 MB, less than 10.00% 
def create_target_array(nums, index)
  result = []
  for i in (0...index.size) do
    result.insert(index[i], nums[i]) 
  end

  result
end
```

[[Competitive Programming/Leetcode/Korean/1389 - Create Target Array in the Given Order | JavaScript solution]]
[[Competitive Programming/Leetcode/English/1389 - Create Target Array in the Given Order | C++ solution]]