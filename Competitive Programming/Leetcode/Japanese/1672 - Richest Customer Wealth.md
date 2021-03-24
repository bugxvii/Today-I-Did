tags: #leetcode #easy #ruby #japanese #array

<hr />

[1672. Richest Customer Wealth](https://leetcode.com/problems/richest-customer-wealth/)

全く同じコードだけどC++とJSはなんでこんなに遅いのかな。多分Rubyで解いた人たちがそんなにないからかな。C++は30％だっだ。

```ruby
# Runtime: 52 ms, faster than 74.77% 
# Memory Usage: 209.8 MB, less than 96.73%

def maximum_wealth(accounts)
  max = 0

  accounts.each do |bank|
	sum = 0
	bank.each do |money|
	  sum += money
	end
	max = sum > max ? sum : max
  end

  max
end
```

[[Competitive Programming/Leetcode/Korean/1672 - Richest Customer Wealth | JavaScript solution]]
[[Competitive Programming/Leetcode/English/1672 - Richest Customer Wealth | C++ solution]]