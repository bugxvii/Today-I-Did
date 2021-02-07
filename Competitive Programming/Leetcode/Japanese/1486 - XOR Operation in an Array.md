tags: #leetcode #easy #ruby #japanese #array #bit-manipulation 

<hr />

[1486. XOR Operation in an Array](https://leetcode.com/problems/xor-operation-in-an-array/)

```rb
# Runtime: 56 ms, faster than 37.50%
# Memory Usage: 210 MB, less than 6.25%
def xor_operation(n, start)
  result = start
  for i in (1...n) do 
    result = result ^ (start + 2*i) 
  end

  result
end
```