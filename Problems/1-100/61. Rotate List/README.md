# 61. Rotate List
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/61.%20Rotate%20List/problem.png"/>


## python solution
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def rotateRight(self, head, k):
        """
        :type head: ListNode
        :type k: int
        :rtype: ListNode
        """
        """
        思路整理
        Input: 1->2->3->4->5->NULL, k = 2
        Output: 4->5->1->2->3->NULL
        1)求整个列表的长度l=5 并找到列表最后一个元素last=5
        2)求出second的长度k=k%2=2 
        presecond的位置由队首移动l-k-1=2个位置得到presecond=3  
        second=presecond.next=4
        3)将presecond.next=None此时dummy->1->2->3->NULL
        last.next=dummy.next此时second=4->5->1->2->3->NULL
        dummy.next=second
        """
        if not head or not head.next or k==0:
            return head
        dummy=ListNode(0)
        dummy.next=head
        last=head
        l=1#列表长度
        while last.next:
            last=last.next
            l+=1
        k=k%l
        if k==0:
            return head
        temp=l-k
        presecond=head
        while temp-1:
            presecond=presecond.next
            temp-=1
        second=presecond.next
        presecond.next=None
        last.next=dummy.next
        dummy.next=second
        return dummy.next
```
