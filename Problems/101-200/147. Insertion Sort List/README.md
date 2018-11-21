# 147. Insertion Sort List
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/147.%20Insertion%20Sort%20List/problem.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/147.%20Insertion%20Sort%20List/example.png"/>



## python solution
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def insertionSortList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if head==None:
            return head
        if head.next==None:
            return head
        helpler=ListNode(0)#已排序的节点的前一个节点
        pre=helpler#在pre和pre.next之间插入新的节点
        cur=head#当前要插入的节点
        next=cur.next#下一次要插入的节点
        while cur:
            next=cur.next
            while pre.next and pre.next.val<cur.val:
                  pre=pre.next
            cur.next=pre.next
            pre.next=cur
            cur=next
            pre=helpler
        return helpler.next
```

## python3 solution
```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def insertionSortList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if head==None:
            return head
        if head.next==None :
            return head
        sort=head
        unsort=head.next
        sort.next=None
        position=sort
        pre=None
        while unsort: 
            while position: 
                if unsort.val>=position.val:
                    if position.next :
                        pre=position
                        position=position.next
                    else:
                        position.next=unsort
                        unsort=unsort.next
                        position.next.next=None
                        position=sort
                        pre=None
                        break     
                else: 
                    if pre:
                        temp=unsort
                        unsort=unsort.next
                        pre.next=temp
                        temp.next=position
                        position=sort
                        pre=None
                        break
                    else:
                        temp=unsort
                        unsort=unsort.next
                        temp.next=position
                        sort=temp
                        position=sort
                        pre=None
                        break
        return sort        
```

