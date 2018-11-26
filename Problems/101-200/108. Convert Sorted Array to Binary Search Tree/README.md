# 108. Convert Sorted Array to Binary Search Tree
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/108.%20Convert%20Sorted%20Array%20to%20Binary%20Search%20Tree/problem.png"/>



## python solution
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def sortedArrayToBST(self, nums):
        """
        :type nums: List[int]
        :rtype: TreeNode
        """
        def helper(nums,lo,hi):
            if (lo>hi):
                return
            mid=int((lo+hi)/2)
            node=TreeNode(nums[mid])
            node.left=helper(nums,lo,mid-1)
            node.right=helper(nums,mid+1,hi)
            return node
        return  helper(nums,0,len(nums)-1)  
```


## python3 solution
```python3
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def sortedArrayToBST(self, nums):
        """
        :type nums: List[int]
        :rtype: TreeNode
        """
        if not nums:
            return None
        def buildBST(nums,root,val):
            if not nums:
                 return
            l=len(nums)
            i=int(l/2) 
            if l>=3:
                root.left=TreeNode(nums[int(i/2)])
                root.right=TreeNode(nums[i+int(i/2) if int(i/2)>l-(i+int(i/2)+1) else i+int(i/2)+1]) 
                buildBST(nums[:i],root.left,root.left.val)
                buildBST(nums[i+1:],root.right,root.right.val)
            if l==2:
                if nums[i-1]==val:
                    root.right=TreeNode(nums[i])
                else:
                    root.left=TreeNode(nums[i-1])
                return
        l=len(nums)
        i=int(l/2) 
        root=TreeNode(nums[i])  
        buildBST(nums,root,root.val)
```
