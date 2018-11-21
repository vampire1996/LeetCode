# 102. Binary Tree Level Order Traversal
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/102.%20Binary%20Tree%20Level%20Order%20Traversal/problem.png"/>

## python solution
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def levelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        res,level=[],[root]
        while level and root:
            res.append([node.val for node in level])
            LRpairs=[(node.left,node.right) for node in level]
            level=[leaf for LR in LRpairs for leaf in LR if leaf]
        return res  
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
    def levelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        res=[]
        if root==None:
            return res

        def traversal(ans,node,level):
            if node ==None:
                return
            a=[]
            if level==len(ans):
               ans.append(a)
            ans[level].append(node.val) 
            traversal(ans,node.left,level+1) 
            traversal(ans,node.right,level+1)  
        traversal(res,root,0)
        return res
```
