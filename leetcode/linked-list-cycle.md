---
description: >-
  Given head, the head of a linked list, determine if the linked list has a
  cycle in it.
---

# Linked List Cycle

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        if not head:
            return False
        slow = head
        fast = head.next
        while True:
            if slow == fast:
                return True
            if not fast or not fast.next:
                return False
            slow = slow.next
            fast = fast.next.next
```
