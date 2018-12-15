# 234. Palindrome Linked List
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## python solution
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def isPalindrome(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        """
        Input: 1->2->2->1      (1)
        Input: 1->2->3->2->1   (2)
        思路整理:
        1)首先找到链表的中间节点slow
        偶数个节点(1) slow=2->2->1
        奇数个节点(2) slow=3->2->1 
        2)翻转链表的第二部分 
        e.g. slow=4->3->2->1  fast=slow.next=3->2->1
         temp=slow.next           temp=3->2->1       temp=2->3->1
         slow.next=fast.next      slow=4->2->1       slow=4->1
         fast.next=fast.next.next fast=3->1          fast=3
         slow.next.next=temp      slow=4->2->3->1    slow=4->1->2->3
        3)比较第一部分和第二部分，完全相同则为回文，否则不是
        Explanation
        1)find the middle find the middle of the linked list
        when the number of nodes are odd slow=2->2->1
        when the number of nodes are even slow=3->2->1
        2)reverse the second part
        3)compare the 1st and the 2nd part
        """
        if not head:return True
        slow,fast=head,head
        #find the middle of the linked list
        while fast.next and fast.next.next:
            slow=slow.next
            fast=fast.next.next
        fast=slow.next
        #reverse the second part
        while fast and fast.next:
            temp=slow.next
            slow.next=fast.next
            fast.next=fast.next.next
            slow.next.next=temp
        #compare the 1st and the 2nd part
        fast=slow.next
        slow=head
        while fast:
            if slow.val!=fast.val:return False
            slow=slow.next
            fast=fast.next
        return True
```

## python3 solution
```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def isPalindrome(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        """
        Input: 1->2->2->1
        Input: 1->2->3->2->1
        思路整理:
        1)rev存储链表的前半部分翻转后的结果 rev=2->1
        slow存储 链表的后半部分 slow=2->1
        2)这种算法并没有改变原链表的结构 而是构建以rev为链表头的链表
        3)当节点数为偶数fast=None slow=2->1
        当节点数为偶数fast=1 slow=3->2->1 因此slow=slow.next=2->1
        """
        rev,fast,slow=None,head,head
        while fast and fast.next:
            fast=fast.next.next
            rev,rev.next,slow=slow,rev,slow.next
        if fast:slow=slow.next
        while rev and rev.val==slow.val:
            rev=rev.next
            slow=slow.next
        return not rev
```

## java solution
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public boolean isPalindrome(ListNode head) {
        if(head==null)return true;
        ListNode slow=head,fast=head;
        while(fast.next!=null&&fast.next.next!=null)
        {
            slow=slow.next;
            fast=fast.next.next;
        }
        fast=slow.next;
        while(fast!=null&&fast.next!=null)
        {
            ListNode next=slow.next;
            slow.next=fast.next;
            fast.next=fast.next.next;
            slow.next.next=next;
        }
        fast=slow.next;
        slow=head;
        while(fast!=null)
        {
            if(fast.val!=slow.val) return false;
            slow=slow.next;
            fast=fast.next;
        }
        return true;
    }
}
```
