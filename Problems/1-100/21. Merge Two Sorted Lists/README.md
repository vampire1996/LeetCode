# 21. Merge Two Sorted Lists
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/21.%20Merge%20Two%20Sorted%20Lists/problem.png"/>

## python solution
```python
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        dummy=ListNode(0)
        pre=dummy
        while l1 or l2:
          if l1 and not l2:
             pre.next=l1
             pre=pre.next
             l1=l1.next
          elif not l1 and l2:
              pre.next=l2
              pre=pre.next
              l2=l2.next
          elif l1 and l2:
            if l1.val<l2.val:
                pre.next=l1
                pre=pre.next
                l1=l1.next
            elif l1.val>l2.val:
                pre.next=l2
                pre=pre.next
                l2=l2.next
            else:
                #此处要提前将l1指向l1.next
                """
                l1=1->2->3
                l2=1->4->5
                pre.next=l1
                pre=0->1->2->3
                l1=l1.next=2->3
                pre.next=l2
                pre=0->1->1->4->5
                """
                pre.next=l1
                l1=l1.next
                pre=pre.next
                pre.next=l2
                pre=pre.next
                l2=l2.next  
        return dummy.next
```

## python3 solution
```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        """
        l1->2->3->4
        l2->1->5->6
        当l1指向空时 返回l2=5->6 作为之前1->2->3->4的next
        """
        #recursive version
        if not l1:return l2
        if not l2:return l1
        if l1.val<l2.val:
            l1.next=self.mergeTwoLists(l1.next, l2)
            return l1
        else:
            l2.next=self.mergeTwoLists(l1, l2.next)
            return l2 
```
