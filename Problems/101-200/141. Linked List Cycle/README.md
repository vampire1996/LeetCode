# 141. Linked List Cycle
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/141.%20Linked%20List%20Cycle/problem.png"/>

## python solution
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        """
        1)如果无环，则fast走到头结束即可
        2）如果有环 fast一直处于环内 slow走到环第一个元素时返回Ture
        """
        if not head or not head.next:
            return False
        slow=head
        fast=slow.next
        while slow.next:
            if not fast:
                return False
            if fast.next==slow:
                return True
            slow=slow.next
            if  fast.next:
                fast=fast.next.next
        return False
```

## c solution
```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
bool hasCycle(struct ListNode *head) {
    if (head==NULL||head->next==NULL)return false;
    struct ListNode *slow=head,*fast=slow->next;
    while(fast->next&&fast->next->next)
    {
        if(fast->next==slow)
            return true;
        fast=fast->next->next;
        slow=slow->next;
    }
    return false;
}  
```
