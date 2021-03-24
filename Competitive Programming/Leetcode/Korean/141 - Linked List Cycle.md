tags: #leetcode #linkedlist #two-pointer #korean #JavaScript #easy

<hr />

[141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

토끼와 거북이 알고리즘 사용.

```js
/** 
 * Runtime: 88 ms, faster than 62.31% 
 * Memory Usage: 41.4 MB, less than 22.21%
 */ 

/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */

/**
 * @param {ListNode} head
 * @return {boolean}
 */
var hasCycle = function(head) {
  if (!head || !head.next) return false;

  let tortoise = head.next;
  let hare = head.next.next;

  for(let i=0; i<10001; ++i) {
    if (tortoise === hare) return true;
    tortoise = tortoise.next;
    if(!tortoise) return false;
    hare = hare.next;
    if(!hare || !hare.next) return false;
    hare = hare.next;
  }

  return false;
};
```

[[Competitive Programming/Leetcode/English/141 - Linked List Cycle | C++ Solution]]
[[Competitive Programming/Leetcode/Japanese/141 - Linked List Cycle | Ruby Solution]]