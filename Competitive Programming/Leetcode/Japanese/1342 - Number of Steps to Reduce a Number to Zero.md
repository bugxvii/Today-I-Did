tags: #leetcode #array #japanese #ruby #easy

<hr />

[1342. Number of Steps to Reduce a Number to Zero](https://leetcode.com/problems/number-of-steps-to-reduce-a-number-to-zero/)

```rb
# Runtime: 48 ms, faster than 84.85%
# Memory Usage: 209.6 MB, less than 70.71%
def number_of_steps (num)
    cnt = 0
    while (num > 0) do 
        if num%2 == 0
            num = num / 2
        else 
            num -= 1
        end
        
        cnt += 1
    end
    cnt
end

# usnig BITWISE OPERATOR
# Runtime: 40 ms, faster than 95.96%
# Memory Usage: 209.6 MB, less than 70.71%
def number_of_steps (num)
    cnt = 0
    while (num > 0) do 
        if num&1 == 0
            num = num >> 1 
        else 
            num -= 1
        end
        
        cnt += 1
    end
    cnt
end
```