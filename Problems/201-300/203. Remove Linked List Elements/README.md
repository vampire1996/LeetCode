# 203. Remove Linked List Elements
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/103.%20Binary%20Tree%20Zigzag%20Level%20Order%20Traversal/problem.png"/>

## python solution
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def removeElements(self, head, val):
        """
        :type head: ListNode
        :type val: int
        :rtype: ListNode
        """
        if not head: return head
        head.next=self.removeElements(head.next, val)
        return head.next if head.val==val else head
```

## python3 solution
```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def removeElements(self, head, val):
        """
        :type head: ListNode
        :type val: int
        :rtype: ListNode
        """
        if not head:
            return head
        dummy=ListNode(0)
        dummy.next=head
        pre=dummy
        cur=pre.next
        while cur:
            if cur.val==val:
                pre.next=cur.next
                cur=pre.next
            else:
                pre=pre.next
                cur=pre.next
        return dummy.next 
```
