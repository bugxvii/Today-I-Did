tags: #leetcode #easy #ruby #japanese #sort

<hr />

[1528. Shuffle String](https://leetcode.com/problems/shuffle-string/)

```rb
# Runtime: 68 ms, faster than 41.18%
# Memory Usage: 210.4 MB, less than 36.97%
def restore_string(s, indices)
    result = 'a' * indices.size
    j = 0
    indices.each do |i|
        result[i] = s[j] 
        j += 1
    end
    
    return result
end
```