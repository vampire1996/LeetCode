# 105. Construct Binary Tree from Preorder and Inorder Traversal
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/105.%20Construct%20Binary%20Tree%20from%20Preorder%20and%20Inorder%20Traversal/problem.png"/>


## python solution
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def buildTree(self, preorder, inorder):
        """
        :type preorder: List[int]
        :type inorder: List[int]
        :rtype: TreeNode
        """
        """
        利用列表的pop操作 将preorder中元素依次取出 因此不需要计算左右子树根节点在preorder中的位置 
        因为始终在队列之首
        """
        if inorder:
            ind=inorder.index(preorder.pop(0))
            node=TreeNode(inorder[ind])
            node.left=self.buildTree(preorder,inorder[:ind])
            node.right=self.buildTree(preorder,inorder[ind+1:])
            return node
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
    def buildTree(self, preorder, inorder):
        """
        :type preorder: List[int]
        :type inorder: List[int]
        :rtype: TreeNode
        """
        """
        preorder: root-left-right
        inorder: left-root-right
        postorder: left-right-root
        """
        """
        思路整理
        1)首先在给定上下限(lo,hi)的中序遍历中找到先序遍历中的preorder[t]对应的inorder[i]
        --代表该左/右子树的根节点
        2)其次将中序遍历inorder[i]之前认为左子树 之后为右子树
        若两子树长度均大于0 则左子树根节点为preorder[t]  
        左子树根节点为preorder[t+i-lo+1]  i-lo代表左子树长度 加一即为右子树根节点
        e.g.
        preorder = [3,9,20,15,7] 根节点 3 t=0 i=1 lo=0 hi=5
        inorder = [9,3,15,20,7] 3左侧[9]左子树  右侧[15 20 7]右子树
        t+1=1--preorder[1]=9--左子树根节点  t+i-lo+1=2--preorder[2]=20--右子树根节点
        """
        l=len(preorder) 
        def helper(lo,hi,t): 
            if lo>=hi:
                return None
            for i in range(lo,hi):
                if inorder[i]==preorder[t]:
                    break      
            root=TreeNode(inorder[i]) 
            if i-lo>0 and hi-i>0:
                root.left=helper(lo,i,t+1)
                root.right=helper(i+1,hi,t+i-lo+1)
            elif i-lo>0 and hi-i==0:
                root.left=helper(lo,i,t+1)
            else:
                root.right=helper(i+1,hi,t+1)
            return root
        return  helper(0,l,0)
```
