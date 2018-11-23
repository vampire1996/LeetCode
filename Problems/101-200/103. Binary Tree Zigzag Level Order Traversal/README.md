# 103. Binary Tree Zigzag Level Order Traversal
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/103.%20Binary%20Tree%20Zigzag%20Level%20Order%20Traversal/problem.png"/>

## python solution
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def zigzagLevelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        res=[]
        if not root:
            return res
        def traversal(ans,node,level):
            if not node:
                return
            if level>=len(ans) and node:
                ans+=[[]]
            ans[level].append(node.val)
            traversal(ans,node.left,level+1)
            traversal(ans,node.right,level+1)
        traversal(res,root,0) 
        l=len(res)
        for i in range(l):
            if i%2==1:
                res[i]=list(reversed(res[i]))
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
"""
栈(stack)--先进后出
队列(heap)--先进先出

python3 没有xrange()
"""

class Solution(object):
    def zigzagLevelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        if not root:
            return []
        flag=1
        stack,temp,res=[root],[],[]
        while stack:
            l=len(stack)
            for i in range(l):
                node=stack.pop(0) 
                """
                服从FILO：First In Last Out
                出栈为:stack.pop(-1)
                
                服从FIFO：First In First Out
                出栈为:stack.pop(0) 实际上和队列一样
                """
                if node:
                    temp.append(node.val)
                if node.left:
                    stack.append(node.left)
                if node.right:
                    stack.append(node.right)
            res.append(temp[::flag])     
            temp=[]
            flag*=-1
        return res
```
