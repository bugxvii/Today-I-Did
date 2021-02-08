tags: #leetcode #easy #ruby #japanese #string

<hr />

[1614. Maximum Nesting Depth of the Parentheses](https://leetcode.com/problems/maximum-nesting-depth-of-the-parentheses/)

カウントしましょう。

```ruby
# Runtime: 48 ms, faster than 94.92%
# Memory Usage: 209.9 MB, less than 64.41%
def max_depth(s)
  max = 0
  cnt = 0

  for i in (0...s.size) do 
	if s[i] == '('
	  cnt += 1
	elsif s[i] == ')'
	  cnt -= 1
	end

	max = (cnt > max) ? cnt : max
  end
  max
end
```

[[Competitive Programming/Leetcode/Korean/1614 - Maximum Nesting Depth of the Parentheses | JavaScript solution]]
[[Competitive Programming/Leetcode/English/1614 - Maximum Nesting Depth of the Parentheses | C++ solution]]