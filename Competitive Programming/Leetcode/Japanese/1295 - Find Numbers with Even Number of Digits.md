tags: #leetcode #array #japanese #ruby #easy

<hr />

[1295. Find Numbers with Even Number of Digits](https://leetcode.com/problems/find-numbers-with-even-number-of-digits/)

```rb
# Runtime: 48 ms, faster than 95.38%
# Memory Usage: 210.2 MB, less than 65.38%

def find_numbers(nums)
  result =  0

  for x in nums do
    if x.to_s.length % 2 == 0
      result += 1
    end
  end

  result
end
```

[[Competitive Programming/Leetcode/Korean/1295 - Find Numbers with Even Number of Digits | JavaScript solution]]
[[Competitive Programming/Leetcode/English/1295 - Find Numbers with Even Number of Digits | C++ solution]]