# 143. Reorder List
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/101.SymmetricTree/problem.png "/>

## python solution
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reorderList(self, head):
        """
        :type head: ListNode
        :rtype: void Do not return anything, modify head in-place instead.
        """
        #  O(n) time O(1) space
        if head and head.next:
            #Find the middle of the list
            p1=head
            p2=head
            while p2.next and p2.next.next:
                p1=p1.next
                p2=p2.next.next
            #Reverse the half after middle  1->2->3->4->5->6 to 1->2->3->6->5->4
            middle=p1
            cur=middle.next
            while cur.next:
                post=cur.next
                cur.next=post.next
                post.next=middle.next
                middle.next=post
            #Start reorder one by one  1->2->3->6->5->4 to 1->6->2->5->3->4    
            p1=head
            p2=middle.next
            while p1!=middle:
                middle.next=p2.next
                p2.next=p1.next
                p1.next=p2
                p1=p2.next
                p2=middle.next
```

## python3 solution
```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reorderList(self, head):
        """
        :type head: ListNode
        :rtype: void Do not return anything, modify head in-place instead.
        """
        #超时了 O(n^2)
        if  head:
         cur=head
         tail=cur.next
         while cur.next:
            if not cur.next.next:
                break
            while tail.next:
                if not tail.next.next and tail.next is not None:
                    beforetail=tail   
                tail=tail.next
            beforetail.next=None
            tail.next=cur.next  
            cur.next=tail
            if cur.next.next:
                cur=cur.next.next
            else:
                break
            tail=cur.next
```
