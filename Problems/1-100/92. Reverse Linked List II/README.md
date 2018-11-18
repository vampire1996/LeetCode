# 92. Reverse Linked List II

<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/92.%20Reverse%20Linked%20List%20II/problem.jpg"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/92.%20Reverse%20Linked%20List%20II/1.jpg"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/92.%20Reverse%20Linked%20List%20II/2.jpg"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/92.%20Reverse%20Linked%20List%20II/3.jpg"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/92.%20Reverse%20Linked%20List%20II/4.jpg"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/92.%20Reverse%20Linked%20List%20II/5.jpg"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/92.%20Reverse%20Linked%20List%20II/6.jpg"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/92.%20Reverse%20Linked%20List%20II/7.jpg"/>

## python solution
```python
class Solution:
    def reverseBetween(self, head, m, n):
        """
        :type head: ListNode
        :type m: int
        :type n: int
        :rtype: ListNode
        """
        if m>=n:
          return head
        dummy=ListNode(0)
        dummy.next=head
        prev=dummy
        i=1
        while i<m:
          prev=prev.next
          i+=1
        cur=prev.next
        post=cur.next
        while i<n:
          cur.next=post.next
          post.next=prev.next
          prev.next=post
          post=cur.next
          i+=1   
        return dummy.next
```
