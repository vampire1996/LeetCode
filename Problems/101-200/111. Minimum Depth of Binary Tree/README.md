# 111. Minimum Depth of Binary Tree
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/100.%20Same%20Tree/problem.png "/>


## python solution
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    left,right=1,1
    def minDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        """
         3
          \
          20
            \
             7
        思路整理:
        针对这种情况 树的最小深度为3
        not root.left and root.right
        递归计算右子树的深度 同时令左子树深度为right+1
        由于只更小的那个数 因此left被舍去
        """
        if not root :
            return 0  
        def helper(root,depth):
            left,right=1,1
            if not root.left and not root.right: return depth
            elif root.left and not root.right:
                left=helper(root.left,depth+1)
                right=left+1
            elif not root.left and root.right:
                right=helper(root.right,depth+1)
                left=right+1
            elif root.left and root.right:
                left=helper(root.left,depth+1)
                right=helper(root.right,depth+1)               
            return left if left<right else right
        return helper(root,1)  
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
    def minDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        """
         3
          \
          20
            \
             7
        思路整理:
        针对这种情况 树的最小深度为3
        left=0 right=2 则舍弃left而取深度为right+left+1
        +1代表树根
        """
        if not root:
            return 0
        left=self.minDepth(root.left)
        right=self.minDepth(root.right)
        return left+right+1 if left==0 or right==0 else min(left,right)+1
```
