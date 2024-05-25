---
share: "true"
---


# Middle of the Linked List

Companies: Microsoft
Date: September 1, 2021
Difficulty: Easy
Review Date: September 29, 2021
Status: Done
Tags: Linked List

```python
from math import ceil, floor

# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def middleNode1(self, head: Optional[ListNode]) -> Optional[ListNode]:
        """Find the middle node and return the index

        Time: O(n)
        Space: O(n)

        """
        nodes = []

        if not head:
            return None
        if not head.next:
            return head

        while head:
            nodes.append(head)
            head = head.next

        numNodes = len(nodes)
        middleNodeIndex = floor(numNodes / 2)

        return nodes[middleNodeIndex]
```

A better solution with less space using [[fast-and-slow pointers|fast-and-slow pointers]]

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def middleNode(self, head: Optional[ListNode]) -> Optional[ListNode]:
        """Find the middle node using fast and slow pointers

        Time: O(n)
        Space: O(1)
        """
        if not head:
            return None
        if not head.next:
            return head

        slowPointer, fastPointer = head, head
        while fastPointer and fastPointer.next:
            slowPointer = slowPointer.next
            fastPointer = fastPointer.next.next

        return slowPointer
```
