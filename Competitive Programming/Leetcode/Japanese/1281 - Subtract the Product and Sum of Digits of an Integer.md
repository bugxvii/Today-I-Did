tags: #leetcode #math #japanese #ruby #easy

<hr />

[1281. Subtract the Product and Sum of Digits of an Integer](https://leetcode.com/problems/subtract-the-product-and-sum-of-digits-of-an-integer/)

簡単な数学問題。

```rb
# Runtime: 44 ms, faster than 83.10%
# Memory Usage: 209.8 MB, less than 7.04%
def subtract_product_and_sum(n)
  p = 1
  s = 0

  while n > 0 do
    t = n % 10
    n /= 10

    p *= t
    s += t
  end

  p - s
end
```

[[Competitive Programming/Leetcode/Korean/1281 - Subtract the Product and Sum of Digits of an Integer | JavaScript solution]]
[[Competitive Programming/Leetcode/English/1281 - Subtract the Product and Sum of Digits of an Integer | C++ solution]]