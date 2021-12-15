---
description: >-
  You are given two non-empty linked lists representing two non-negative
  integers. The digits are stored in reverse order, and each of their nodes
  contains a single digit. Add the two numbers and return
---

# Add Two Numbers

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        track = 0
        one = 0
        while l1:
            one = l1.val * (10 ** track) + one
            l1 = l1.next
            track += 1
        two = 0
        track = 0
        while l2:
            two = l2.val * (10 ** track) + two
            l2 = l2.next
            track += 1
        three = one + two
        new = ListNode(three % 10, None)
        ptr = new
        three = three // 10
        while three > 0:
            temp = ListNode(three % 10, None)
            three = three // 10
            new.next = temp
            new = new.next
        return ptr
```
