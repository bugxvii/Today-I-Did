tags: #leetcode #array #japanese #ruby #easy

<hr />

[1431. Kids With the Greatest Number of Candies](https://leetcode.com/problems/kids-with-the-greatest-number-of-candies/)

キャンディのmaxを最初に見つけて、それを使ってboolリストの作った。

```rb
# Runtime 56ms
# Faster than 52.02%
# Memory Usage: 210MB, less than 76.88%
def kids_with_candies(candies, extra_candies)
    max = candies.max
    result = []
    
    for x in candies do
       if x + extra_candies >= max then result << true else result << false end 
    end
    result
end
```