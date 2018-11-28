# 82. Remove Duplicates from Sorted List II
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/82.%20Remove%20Duplicates%20from%20Sorted%20List%20II/problem.png"/>

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
        """
        思路整理
        Input: 1->1->1->2->3
        Output: 2->3
        pre->1->1->1->2->3 cur=1->1->1->2->3
        若 cur.val==cur.next.val 则pre->1->2->3 cur=1->2->3  
        temp=1
        若 cur.val==temp 则pre->2->3 cur=2->3
        """
        if not head:
            return head
        dummy=ListNode(0)
        dummy.next=head
        pre=dummy
        cur=pre.next
        temp=0.1
        while cur.next:
            if cur.val==cur.next.val:
                temp=cur.val
                if cur.next.next:
                    pre.next=cur.next.next
                    cur=pre.next
                else:
                    pre.next=None
                    break
            elif cur.val==temp:
                pre.next=cur.next
                cur=pre.next
            else:
                pre=pre.next
                cur=pre.next
        if cur.val==temp:  
            pre.next=None
        return dummy.next         
```
