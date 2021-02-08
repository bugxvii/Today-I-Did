tags: #leetcode #linkedlist #englsh #cpp #easy

<hr />

[237. Delete Node in a Linked List](https://leetcode.com/problems/delete-node-in-a-linked-list/)

```cpp
/**
 * Runtime: 20 ms, faster than 53.79%
 * Memory Usage: 8 MB, less than 52.59%
 */

/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
  public:
    void deleteNode(ListNode* node) {
      node->val = node->next->val;
      ListNode *temp = node->next;
      node->next = node->next->next;
      delete temp;
    }
};

/**
 * Runtime: 20 ms, faster than 53.79%
 * Memory Usage: 8 MB, less than 52.59%
 */

class Solution {
  public:
    void deleteNode(ListNode* node) {
      node->val = node->next->val;
      ListNode *temp = node->next;
      node->next = node->next->next;
      delete temp;
    }
};
```