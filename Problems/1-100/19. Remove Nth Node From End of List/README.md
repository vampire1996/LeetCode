# 19. Remove Nth Node From End of List
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/19.%20Remove%20Nth%20Node%20From%20End%20of%20List/problem.png"/>

## python solution
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def removeNthFromEnd(self, head, n):
        """
        :type head: ListNode
        :type n: int
        :rtype: ListNode
        """
        fast=slow=head
        for i in range(n):
          fast=fast.next
        if not fast:
            return head.next
        while fast.next:
            fast=fast.next
            slow=slow.next
        slow.next=slow.next.next
        return head
```

## python3 solution
```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def removeNthFromEnd(self, head, n):
        """
        :type head: ListNode
        :type n: int
        :rtype: ListNode
        """
        pre=head
        cur=pre 
        total=0
        while cur:
          cur=cur.next
          total+=1
        l=total-n 
        if l==0:
            return head.next
        cur=pre
        post=cur.next   
        while l>1:
            post=cur.next
            cur=cur.next
            l-=1   
        post=cur.next    
        cur.next=post.next    
        return pre
```
