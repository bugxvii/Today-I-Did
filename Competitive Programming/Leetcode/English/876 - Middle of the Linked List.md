tags: #leetcode #linkedlist #english #cpp #easy

<hr />

[876. Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/)

find and return the middle node from the given list.

```cpp
/**
 * Runtime: 0 ms, faster than 100.00%
 * Memory Usage: 7.1 MB, less than 27.55%
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
    ListNode* middleNode(ListNode* head) {
      int size = 0;

      ListNode *temp = head;

      while(temp)
      {
        ++size;
        temp = temp->next;
      }

      size >>= 1;
      temp = head;
      for(int i=0;i<size; ++i)
      {
        temp = temp->next;
      }

      return temp;
    }
};
```