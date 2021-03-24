tags: #leetcode #tree #DFS #recursion #english #cpp #easy

<hr />

[938. Range Sum of BST](https://leetcode.com/problems/range-sum-of-bst/)

Used DFS to traverse the tree within the given range.

```cpp
/**
 * Runtime: 168 ms, faster than 87.27%
 * Memory Usage: 65.1 MB, less than 78.96%
 */

/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
  public:
    int rangeSumBST(TreeNode* root, int low, int high) {
      if(!root) return 0;

      int sum = 0;
      if (root->val >= low && root->val <= high) sum = root->val;
      if (root->val > low) sum += rangeSumBST(root->left, low, high);
      if (root->val < high) sum += rangeSumBST(root->right, low, high);

      return sum;
    }
};
```

[[Competitive Programming/Leetcode/Korean/938 - Range Sum of BST | JavaScript solution]]
[[Competitive Programming/Leetcode/Japanese/938 - Range Sum of BST | Ruby solution]]