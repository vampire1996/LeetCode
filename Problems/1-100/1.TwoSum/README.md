# 1. Two Sum
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## python solution
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def sumNumbers(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        res=[]
        if not root:
            return 0 
        def traversal(res,root,num):
            num+=root.val
            if not root.left and not root.right:
                res.append(num)
                return
            if root.left:
                 traversal(res,root.left,num*10)
            if root.right:
                 traversal(res,root.right,num*10)
        traversal(res,root,0)    
        return sum(res)
```

## python3 solution
```python3
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    total=0
    def sumNumbers(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root:
            return 0 
        def DFS(root,sum):
            sum=sum*10+root.val
            if not root.left and not root.right:
                self.total+=sum
                return 
            if root.left:
                 DFS(root.left,sum)
            if root.right:
                 DFS(root.right,sum)
        DFS(root,0)            
        return self.total
```
