# 24. Swap Nodes in Pairs
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/24.%20Swap%20Nodes%20in%20Pairs/problem.png"/>

## c solution
```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */

struct ListNode* swapPairs(struct ListNode* head) {
    struct ListNode **pp=&head,*a,*b;
    //*pp == a -> b -> (b->next) to *pp == b -> a -> (b->next)
    /*
    注意:不能使用单指针*pp=head 这样pp移动的同时head也会移动 最后返回head不是队首 
    **pp=&head  pp是一个指向指针head地址的指针 而*pp是指向head所指内容的指针 **pp则取出该内容
    */
    while((a=*pp)&&(b=a->next))
    {
        a->next=b->next;
        b->next=a;
        *pp=b;
        pp=&(a->next);//moves pp to the next pair.
    }
    return head;
}
```

## python solution
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def swapPairs(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        """
        Input:1->2->3->4
        思路整理:
        pre=0->1->2->3->4 cur=1->2->3->4
        1)pre.next=cur.next pre=0->2->3->4
        2)cur.next=cur.next.next cur=1->3->4
        3)pre.next.next=cur pre=0->2->1->3->4
        4)pre=cur pre=1->3->4
        5)cur=cur.next cur=3->4
        """
        dummy=ListNode(0)
        dummy.next=head
        pre=dummy
        cur=pre.next
        while cur and cur.next:
            pre.next=cur.next
            cur.next=cur.next.next
            pre.next.next=cur
            pre=cur
            cur=cur.next
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
    #self指向实例类
    def swapPairs(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        #pre -> a -> b -> b.next to pre -> b -> a -> b.next
        pre,pre.next=self,head
        while pre.next and pre.next.next:
            a=pre.next
            b=pre.next.next
            a.next,b.next,pre.next=b.next,a,b#change all three at once
            pre=a
        return self.next
```
