tags: #leetcode #linkedlist #english #cpp #easy

<hr />

[206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

recursion was quite confusing; in fact, it still does...

Iterative:
```cpp
/**
 * Runtime: 20 ms, faster than 6.18%
 * Memory Usage: 8.6 MB, less than 66.45%
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
    ListNode* reverseList(ListNode* head) {
      ListNode *prev = nullptr;
      ListNode *curr = head;

      while (curr != nullptr) {
        ListNode *temp = curr->next;
        curr->next = prev;
        prev = curr;
        curr = temp;
      }

      return prev;
    }
};
```

recursive:
```cpp
/**
 * Runtime: 4 ms, faster than 97.92%
 * Memory Usage: 9 MB, less than 9.56%
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
    ListNode* reverseList(ListNode* head) {
      if (head == nullptr || head->next == nullptr) return head;

      ListNode *p = reverseList(head->next);
      head->next->next = head;
      head->next = nullptr;
      return p;
    }
};
```

[[Competitive Programming/Leetcode/Korean/206 - Reverse Linked List | JavaScript solution]]
[[Competitive Programming/Leetcode/Japanese/206 - Reverse Linked List | Ruby s olution]]