---
share: "true"
---

# Linked List Cycle

Companies: Amazon, Apple, Bloomberg, Goldman Sachs, Google, Microsoft
Date: August 30, 2021
Difficulty: Easy
Review Date: September 29, 2021
Status: Done
Tags: Linked List

Check for proofs in OneNote Algorithms notebooks

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: ListNode) -> bool:
		"""Check if a linked list has cycles

		Time: O(n)
		Space: O(1)
		"""

        if not head:
            return False

        slowPointer = head
        fastPointer = head

        while slowPointer.next and fastPointer.next:
            slowPointer = slowPointer.next
            if fastPointer.next.next:
                fastPointer = fastPointer.next.next
            else:
                return False

            if slowPointer and (slowPointer == fastPointer):
                return True

        return False
```
