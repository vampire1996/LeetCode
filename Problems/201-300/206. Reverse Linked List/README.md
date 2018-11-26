# 206. Reverse Linked List
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/201-300/206.%20Reverse%20Linked%20List/problem.png"/>

## python solution
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head:
            return head
        dummy=ListNode(0)
        cur=head
        dummy.next=cur
        post=cur.next
        while cur.next:
              cur.next=post.next
              post.next=dummy.next
              dummy.next=post
              post=cur.next
        return  dummy.next  
```

## python3 solution
```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

#recursion version
class Solution:
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        """
        1->2->3
        eg 2->3 head: 2, head->next: 3, head->next->next: 3->next
        so head->next->next = head; is to set 3->next = 2, ie. setting 2<-3
        下一步
        1->2 head: 1, head->next: 2, head->next->next: 2->next
        so head->next->next = head; is to set 2->next = 1, ie. setting 1<-2
        由于同时3->2
        所以node=3->2->1
        """

        if not head or not head.next:
            return head
        node=self.reverseList(head.next)
        head.next.next=head
        head.next=None
        return node
```
