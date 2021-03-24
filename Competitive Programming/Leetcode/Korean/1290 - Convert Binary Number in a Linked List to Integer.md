tags: #leetcode #linkedlist #bit-manipulation #korean #JavaScript #easy

<hr />

[1290. Convert Binary Number in a Linked List to Integer](https://leetcode.com/problems/convert-binary-number-in-a-linked-list-to-integer/)

숫자를 2로 곱하면서 비트값을 더해주면 된다.

```js
/**
 * Runtime: 68 ms, faster than 97.66%
 * Memory Usage: 38.6 MB, less than 52.36%
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
 * @return {number}
 */
var getDecimalValue = function(head) {
  let result = 0;

  while (true) {
    result = result * 2 + head.val;
    if (head.next === null) break;
    head = head.next;
  }

  return result;
};
```

[[Competitive Programming/Leetcode/English/1290 - Convert Binary Number in a Linked List to Integer | C++ solution]]
[[Competitive Programming/Leetcode/Japanese/1290 - Convert Binary Number in a Linked List to Integer | Ruby solution]]