tags: #leetcode #linkedlist #japanese #ruby #easy

<hr />

[237. Delete Node in a Linked List](https://leetcode.com/problems/delete-node-in-a-linked-list/)

与えられたノードの次のノードを使えば簡単に解決できる。

```rb
# Runtime: 148 ms, faster than 5.41%
# 210.2 MB

# Definition for singly-linked list.
# class ListNode
#     attr_accessor :val, :next
#     def initialize(val)
#         @val = val
#         @next = nil
#     end
# end

# @param {ListNode} node
# @return {Void} Do not return anything, modify node in-place instead.
def delete_node(node)
  node.val = node.next.val
  node.next = node.next.next
end
```