tags: #leetcode #array #korean #JavaScript #easy

<hr />

[1431. Kids With the Greatest Number of Candies](https://leetcode.com/problems/kids-with-the-greatest-number-of-candies/)

우선 보유하고 있는 사탕의 최댓값을 먼저 구한 다음, 이 값을 이용해서 불린 리스트를 채워나가면 된다.

```js
/**
 * Runtime: 76 ms, faster than 84.03% 
 * Memory Usage: 38.7 MB, less than 7.03%
 */
var kidsWithCandies = function(candies, extraCandies) {
    let max = Math.max(...candies);
    let result = [];
    
    for (let i=0; i<candies.length; ++i)
        if (candies[i] + extraCandies >= max)
            result.push(true);
        else
            result.push(false);
    return result;
};

/**
 * Runtime: 80 ms, faster than 62.62%
 * Memory Usage: 38.9 MB, less than 7.03%
 */
var kidsWithCandies = function(candies, extraCandies) {
    let max = Math.max(...candies);
    let result = [];
    
    candies.forEach(e => {
        result.push(((e + extraCandies) >= max) ? true : false);
    })
    
    return result;
};
```

[[Competitive Programming/Leetcode/English/1431 - Kids With the Greatest Number of Candies | C++ solution]]
[[Competitive Programming/Leetcode/Japanese/1431 - Kids With the Greatest Number of Candies | Ruby solution]]