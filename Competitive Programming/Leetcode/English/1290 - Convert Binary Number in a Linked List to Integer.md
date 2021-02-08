tags: #leetcode #linkedlist #bit-manipulation #english #cpp #easy

<hr />

[1290. Convert Binary Number in a Linked List to Integer](https://leetcode.com/problems/convert-binary-number-in-a-linked-list-to-integer/)

multiply the current number by two every time and add the current bit which is either 0 or 1.

```cpp
/**
 * Runtime: 0 ms, faster than 100.00% 
 * Memory Usage: 8.7 MB, less than 59.80%
 */

/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
  public:
    int getDecimalValue(ListNode* head) {
      unsigned long result = 0;

      while (true)
      {
        result = result  << 1 + head->val;
        head = head->next;

        if (head == NULL || head == nullptr) break;
      }

      return result;
    }
};
```