# 109. Convert Sorted List to Binary Search Tree
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/63.%20Unique%20Paths%20II/problem.png"/>


## python solution
```python
     
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

