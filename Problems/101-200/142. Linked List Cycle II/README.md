# 142. Linked List Cycle II
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/142.%20Linked%20List%20Cycle%20II/problem.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/142.%20Linked%20List%20Cycle%20II/example.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/142.%20Linked%20List%20Cycle%20II/followup.png"/>

## python solution
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def detectCycle(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        """
        思路整理:
        利用字典(hashmap) 存储链表的节点，如果node在dict中未出现,则继续后移node指针
        如果已出现，这说明有环路,返回该node即可(第一次遇到的即为环路的首元素)
        Explanation
        use dictionary to store the nodes in linked list,if current node is not
        in dict,move the pointer to next node
        if it's in the dict alraedy,just return the current node
        (the first node which is in the dict alraedy is the 1st node in the cycle)
        """
        if not head:return None
        node=head
        dict1={}
        while node:
            if dict1.get(node,None)==None:
                #get()返回指定键的值，如果值不在字典中返回默认值(此处为None)
                dict2={node:node.val}
                dict1.update(dict2)#把字典dict2的键/值对更新到dict1里
            else: return node
            node=node.next
        return None
```

## java solution
```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
//Floyd's algorithm

//                  a        b 
//         start ------->-------->meeting
//                      |         |
//                      <----------
//                           c
//         assume fast and slow meets at k steps
//         k=a+b+r1(b+c) slow runs r1 cycles
//         2k=a+b+r2(b+c) fast runs r2 cycles
//         2k=a+b+r2(b+c)=2a+2b+2r1(b+c)
//         (b+c)(r2-2r1)=a+b => (b+c)n=a+b
//         a=(n-1)b+nc=(n-1)(b+c)+c which means when slow moves (n-1) cycles and c, start moves a
/*
不一定要 a = c 满足a = (n-1)(b+c)+c这个式子就可以， 快指针返回头节点，慢指针在原地不
动，然后两个指针在一起一同样的速度走，如果a很长环很小，就说明慢指针可能在环里走了好多圈才
等来了快指针
*/
public class Solution {
    public ListNode detectCycle(ListNode head) {
        if(head==null)return null;
        ListNode fast=head,slow=head;
        while(fast.next!=null&&fast.next.next!=null)
        {
            slow=slow.next;
            fast=fast.next.next;
            if(slow==fast)//有环路
            {
                slow=head;
                while(slow!=fast)
                {
                    slow=slow.next;
                    fast=fast.next;
                }
                return slow;
            }
        }
        return null;
    }
}
```
