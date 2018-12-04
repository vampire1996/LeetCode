# 86. Partition List
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/86.%20Partition%20List/problem.png "/>

## python solution
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def partition(self, head, x):
        """
        :type head: ListNode
        :type x: int
        :rtype: ListNode
        """
        if not head:return head
        greathead,smallhead=ListNode(0),ListNode(0)
        great,small=greathead,smallhead
        while head:
            if head.val>=x:
                great.next=head
                great=great.next
            else:
                small.next=head
                small=small.next
            head=head.next
        """
        great.next=None
        Failing to do this would result in an unterminated, cyclic list.
        Consider 10 -> 1 -> 2 -> 3 with x equal 5. The resulting list would be
        1 -> 2 -> 3 -> 10 -> 1 -> 2 -> 3 -> 10 -> 1 ...

        This is because the 10 node's next has never been changed from pointing to 1 as 
        it was in the original input list. Setting it to null will terminate the list and avoid the cycle.
        """
        small.next=greathead.next
        great.next=None
        return smallhead.next
```

## python3 solution
```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def partition(self, head, x):
        """
        :type head: ListNode
        :type x: int
        :rtype: ListNode
        """
        """
        Input  [1,4,3,2,1,2,4,2,5,4,3] 3
        小于x的部分:prefix->pre1->cur
        大于等于x的部分head2=4->3->4->5->4->3=tail2
        思路整理
        1)首先找到大于等于x的第一个元素 作为第二部分的首元素--head2
        2)遍历列表:
        i.如果cur.val>=x:
           head2->tail2->None =>head2->cur=tail2->None
        ii.如果cur.val<x:
           prefix->pre1->cur->head2->tail2->None
           pre1=pre.next
        Explanation
        1)find the first  element whilch is bigger or equal to x
        take it as the head of the second part
        2)traverse the linked list
        i.if cur.val>=x:head2->tail2->None =>head2->cur=tail2->None
        ii.if cur.val<x:
           prefix->pre1->cur->head2->tail2->None
           pre1=pre.next
        """
        if not head:return head
        dummy=self 
        dummy.next=head
        pre1=dummy
        head2=head
        while head2.next:
            if head2.val>=x:break
            pre1=pre1.next
            head2=head2.next
        cur=head2.next
        tail2=head2
        tail2.next=None
        while cur:
            if cur.val>=x:
                tail2.next=cur
                tail2=tail2.next
                cur=cur.next
                """
                注意这里必须将tail->None
                因为 上面三句结束之后tail->cur
                但当cur.val<x
                pre1->cur 若不将tail->None 则tail->pre1将构成一个环
                """
                tail2.next=None
            else:
                pre1.next=cur
                cur=cur.next
                pre1.next.next=head2
                pre1=pre1.next
        return dummy.next
```
