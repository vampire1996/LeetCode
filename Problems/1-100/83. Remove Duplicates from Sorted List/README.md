# 83. Remove Duplicates from Sorted List
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/83.%20Remove%20Duplicates%20from%20Sorted%20List/problem.png"/>

## python solution
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def deleteDuplicates(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head or not head.next:
            return head
        head.next=self.deleteDuplicates(head.next)
        return head.next if head.val==head.next.val else head
```

## python3 solution
```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def deleteDuplicates(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head or not head.next:
            return head
        pre=head
        cur=pre.next
        while cur:
            if pre.val==cur.val:
                pre.next=cur.next
                cur=pre.next
            else:
                pre=pre.next
                cur=pre.next
        return head
```

