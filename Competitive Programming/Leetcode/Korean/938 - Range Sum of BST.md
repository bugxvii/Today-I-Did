tags: #leetcode #tree #DFS #recursion #korean #JavaScript #easy

<hr />

[938. Range Sum of BST](https://leetcode.com/problems/range-sum-of-bst/)

주어진 범위 내에서 트리를 DFS로 순회했다.

```js
/**
 * Runtime: 236 ms, faster than 34.78%
 * Memory Usage: 65.2 MB, less than 78.43%
 */

/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @param {number} low
 * @param {number} high
 * @return {number}
 */
var rangeSumBST = function(root, low, high) {
  if (!root) return 0;
  let sum = 0;
  if (root.val >= low && root.val <= high) sum = root.val;

  return sum + rangeSumBST(root.left, low, high) + rangeSumBST(root.right, low, high);
};
```

[[Competitive Programming/Leetcode/English/938 - Range Sum of BST | C++ solution]]
[[Competitive Programming/Leetcode/Japanese/938 - Range Sum of BST | Ruby solution]]