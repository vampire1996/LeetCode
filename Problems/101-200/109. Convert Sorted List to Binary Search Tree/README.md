# 109. Convert Sorted List to Binary Search Tree
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/109.%20Convert%20Sorted%20List%20to%20Binary%20Search%20Tree/problem.png"/>

## python solution
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def sortedListToBST(self, head):
        """
        :type head: ListNode
        :rtype: TreeNode
        """
        """
        思路整理:
        Input:[-10,-3,0,5,9]
        1)利用两个指针fast(每次步进两个位置)slow(每次步进一个位置) 找到链表的中点slow作为根节点(0)
        2)将slow其之前一位pre(-3)指向None 则-10->-3->None作为左子树进行递归 5->9->None作为右子树进行递归
        3)返回节点temp
        4)注意当输入节点node.next=None时 返回TreeNode(node.val)   
        How to solve
        1)use two pointer fast and slow which respectly move two position and one position for each time
        find the middle point in the list(0) and  take it as the root of the tree
        2)the pointer per which is the position before slow,let it point to None
        Thus we take -10->-3->None as our left child and use it in recursion,
        meanwhile we take 5->9->None as our right child and use it in recursion
        3)return the node temp
        4)To be noticed,when node.next=None,we just return TreeNode(node.val)   
        """
        if not head: return None
        def helper(node):
             if not node:return  
             if not node.next:return TreeNode(node.val)   
             pre=self
             slow=node
             fast=node
             pre.next=slow
             while fast and fast.next:
                pre=pre.next
                slow=slow.next
                fast=fast.next.next
             pre.next=None
             temp=TreeNode(slow.val)
             temp.left=helper(node)
             temp.right=helper(slow.next)
             return temp
        return helper(head)
```

## python3 solution
```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def sortedListToBST(self, head):
        """
        :type head: ListNode
        :rtype: TreeNode
        """
        if not head: return None
        def helper(lo,hi,nums):
            if lo>hi:return  
            mi=int((lo+hi)/2)
            node=TreeNode(nums[mi])
            node.left=helper(lo,mi-1,nums)
            node.right=helper(mi+1,hi,nums)
            return node
        nums=[]
        while head.next:
            nums.append(head.val)
            head=head.next
        nums.append(head.val)
        return helper(0,len(nums)-1,nums)
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
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode sortedListToBST(ListNode head) {
        if (head==null) return null;
       return helper(head,null);
    }
    public TreeNode helper(ListNode head,ListNode tail)
    {
        if(head==tail) return null;
        ListNode slow=head;
        ListNode fast=head;
        while(fast!=tail&&fast.next!=tail)
        {
            fast=fast.next.next;
            slow=slow.next;
        }
        TreeNode root=new TreeNode(slow.val);
        root.left=helper(head,slow);
        root.right=helper(slow.next,tail);
        return root;
    }
}
```

