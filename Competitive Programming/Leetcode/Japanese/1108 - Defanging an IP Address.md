tags: #leetcode #string #japanese #ruby #easy

<hr />

[1108. Defanging an IP Address](https://leetcode.com/problems/defanging-an-ip-address/)

文字を探してreplaceする。

```rb
=begin
Runtime: 44ms, faster than 83.48%
Memory Usage: 209.8 MB
=end
def defang_i_paddr(address)
    i = 1
    while (i < address.length) do
        if address[i-1] == '.'
            address.insert(i-1, '[')
            address.insert(i+1, ']')
            i += 2
        end
        i += 1
    end
    address
end
```

[[Competitive Programming/Leetcode/Korean/1108 - Defanging an IP Address | JavaScrpit solution]]
[[Competitive Programming/Leetcode/English/1108 - Defanging an IP Address | C++ solution]]