tags: #leetcode #easy #cpp #english #string

<hr />

[1662. Check If Two String Arrays are Equivalent](https://leetcode.com/problems/check-if-two-string-arrays-are-equivalent/)
    
iterate the vector and compare each character

```cpp
/**
 * Runtime: 4 ms, faster than 66.67%
 * Memory Usage: 11.8 MB, less than 33.33%
 */
class Solution {
  public:
    bool arrayStringsAreEqual(vector<string>& word1, vector<string>& word2) {
      string str1 = "";
      string str2 = "";

      for (string s : word1) 
        str1 += s;

      for (string s : word2) 
        str2 += s;

      if (str1.size() != str2.size()) 
        return false;
      else
      {    
        for (int i=0; i<str1.size(); ++i)
        {
          if (str1[i] != str2[i])
            return false;
        }
      }

      return true;
    }
};
```