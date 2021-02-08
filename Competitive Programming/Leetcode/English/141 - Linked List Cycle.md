tags: #leetcode #linkedlist #two-pointer #english #cpp #easy

<hr />

[141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

the tortoise and the hare algorithm.

```cpp
/*
 * Runtime: 8 ms, faster than 69.66% 
 * Memory Usage: 7.8 MB, less than 80.97%
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
    bool hasCycle(ListNode *head) {
      if (!head) return false;
      if (!head->next) return false;

      ListNode *tortoise = head->next;
      ListNode *hare = head->next->next;

      for(int i=0; i<10001; ++i) {
        if (tortoise == hare) return true;
        tortoise = tortoise->next;
        if (!tortoise) return false;
        hare = hare->next;
        if(!hare || !hare->next) return false;
        hare = hare->next;
      }

      return false;
    }
};
```

[[Competitive Programming/Leetcode/Korean/141 - Linked List Cycle | JavaScript solution]]
[[Competitive Programming/Leetcode/Japanese/141 - Linked List Cycle | Ruby solution]]