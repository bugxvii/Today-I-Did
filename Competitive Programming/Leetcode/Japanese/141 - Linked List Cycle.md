tags: #leetcode #linkedlist #two-pointer #japanese #ruby #easy

<hr />

[141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

ウサギとカメ「The Tortoise and the Hare」というアルゴリズムを使う。
```rb
# Runtime: 56 ms, faster than 92.38% 
# Memory Usage: 210.5 MB, less than 67.62%
#
# Definition for singly-linked list.
# class ListNode
#     attr_accessor :val, :next
#     def initialize(val)
#         @val = val
#         @next = nil
#     end
# end

# @param {ListNode} head
# @return {Boolean}
def hasCycle(head)
  return false if !head or !head.next

  tortoise = head.next
  hare = head.next.next

  0.upto(10000) do |_|
    return true if tortoise == hare

    tortoise = tortoise.next
    return false if !tortoise

    hare = hare.next
    return false if !hare or !hare.next
    hare = hare.next
  end

  false
end
```