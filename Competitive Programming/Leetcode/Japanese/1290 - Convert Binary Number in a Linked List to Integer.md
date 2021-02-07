tags: #leetcode #linkedlist #bit-manipulation #japanese #ruby #easy

<hr />

[1290. Convert Binary Number in a Linked List to Integer](https://leetcode.com/problems/convert-binary-number-in-a-linked-list-to-integer/)

毎回数を2倍して、ビット(`1`または`0`)を足したらオッケー。

```rb
# Runtime: 60 ms, faster than 27.73%
# Memory Usage: 209.9 MB, less than 29.41%

# Definition for singly-linked list.
# class ListNode
#     attr_accessor :val, :next
#     def initialize(val = 0, _next = nil)
#         @val = val
#         @next = _next
#     end
# end
# @param {ListNode} head
# @return {Integer}
def get_decimal_value(head)
  result = 0

  while true do
    result = result * 2 + head.val
    head = head.next

    break if head == nil
  end

  result
end
```