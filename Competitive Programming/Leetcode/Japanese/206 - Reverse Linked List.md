tags: #leetcode #linkedlist #japanese #ruby #easy

<hr />

[206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

簡単な問題だと思ったのに…難しかった。単純なiterativeの場合はなんとなく絵を描けながらできたけどrecursiveは全然無理だった。もっと勉強しなきゃ！

Iterative:
```rb
# Runtime: 96 ms, faster than 7.00%
# Memory Usage: 210.4 MB, less than 37.74%

# Definition for singly-linked list.
# class ListNode
#     attr_accessor :val, :next
#     def initialize(val = 0, _next = nil)
#         @val = val
#         @next = _next
#     end
# end
# @param {ListNode} head
# @return {ListNode}
def reverse_list(head)
  prev = nil
  curr = head

  while(curr != nil) do
    temp = curr.next
    curr.next = prev
    prev = curr
    curr = temp
  end

  return prev
end
```

recursion:
```rb
# Runtime: 52 ms, faster than 83.27%
# Memory Usage: 210.7 MB, less than 15.56%

# Definition for singly-linked list.
# class ListNode
#     attr_accessor :val, :next
#     def initialize(val = 0, _next = nil)
#         @val = val
#         @next = _next
#     end
# end
# @param {ListNode} head
# @return {ListNode}
def reverse_list(head)
  return head if head==nil or head.next==nil

  p = reverse_list(head.next)
  head.next.next = head
  head.next = nil
  p
end
```