tags: #leetcode #string #english #cpp #easy

<hr />

[1108. Defanging an IP Address](https://leetcode.com/problems/defanging-an-ip-address/)

find and replace.

```cpp
/**
 * Runtime: 0 ms, faster than 100.00%
 * Memory Usage: 6.1 MB, less than 86.04%
 */
class Solution {
public:
    string defangIPaddr(string address) {
        string s = "";
        for(int i=0; address[i]; ++i)
        {
            if(address[i] != '.') s += address[i];
            else 
            {
                s += "[.]";
                
            }
        }
        
        return s;
    }
};
```

[[Competitive Programming/Leetcode/Korean/1108 - Defanging an IP Address | JavaScript solution]]
[[Competitive Programming/Leetcode/Japanese/1108 - Defanging an IP Address | Ruby solution]]