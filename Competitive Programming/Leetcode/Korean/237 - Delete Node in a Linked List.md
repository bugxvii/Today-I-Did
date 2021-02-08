tags: #leetcode #linkedlist #korean #JavaScript #easy

<hr />

[237. Delete Node in a Linked List](https://leetcode.com/problems/delete-node-in-a-linked-list/)

삭제 할 노드외에는 아무것도 주어지지 않는 상태에서, 주어진 노드를 삭제.

```js
/** 
 * Runtime: 84 ms, faster than 82.95%
 * Memory Usage: 40 MB, less than 95.37%
 */

/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} node
 * @return {void} Do not return anything, modify node in-place instead.
 */
var deleteNode = function(node) {
  node.val = node.next.val;
  node.next = node.next.next;
};
```

[[Competitive Programming/Leetcode/English/237 - Delete Node in a Linked List | C++ solution]]
[[Competitive Programming/Leetcode/Japanese/237 - Delete Node in a Linked List | Ruby solution]]