tags: #leetcode #linkedlist #korean #JavaScript #easy

<hr />

[206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

반복문은 괜찮았는데 재귀로 구현하는게 되게 헷갈렸다. 재귀 나름 이해했다고 생각했는데 좀 더 공부해야 겠다.

iterative:
```js
/**
 * Runtime: 88 ms, faster than 32.32%
 * Memory Usage: 40.7 MB, less than 37.74%
 */

/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var reverseList = function(head) {
  let prev = null;
  let curr = head;

  while(curr != null) {
    let temp = curr.next;
    curr.next = prev;
    prev = curr;
    curr = temp;
  }

  return prev;
};
```

recursive:
```js
/**
 * Runtime: 120 ms, faster than 5.15%
 * Memory Usage: 40.7 MB, less than 37.74%
 */

/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var reverseList = function(head) {
  if (head == null || head.next == null) return head;

  let p = reverseList(head.next);
  head.next.next = head;
  head.next = null;
  return p;
};
```

[[Competitive Programming/Leetcode/English/206 - Reverse Linked List | C++ solution]]
[[Competitive Programming/Leetcode/Japanese/206 - Reverse Linked List | Ruby solution]]