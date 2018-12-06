# 98. Validate Binary Search Tree
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
    def isValidBST(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        if not root:return True
        """
        前序遍历：根结点 ---> 左子树 ---> 右子树
        中序遍历：左子树---> 根结点 ---> 右子树
        后序遍历：左子树 ---> 右子树 ---> 根结点
        思路整理:
        1)对二叉树进行中序遍历 将其存储于res
        2)判断res是否为严格升序排列，如果是则为BST，否则不是
        Explanation:
        1)take a preorder traversal for the binary tree and 
        store the result in array res
        2)if res is in ascend order,return ture,else return false
        """
        def inorderTraversal(node,res):
            if not node:return 
            if node.left:inorderTraversal(node.left,res)
            res.append(node.val)
            if node.right:inorderTraversal(node.right,res)
        res=[]
        inorderTraversal(root,res)
        for i in range(1,len(res)):
             if res[i]<=res[i-1]: return False    
        return True 
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
    def isValidBST(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        #Morris Traversal--inOrder Traversal
        stack=[]
        pre=None
        while root or stack:
            while root:
                stack.append(root)
                root=root.left
            root=stack.pop(-1)#取出栈顶元素
            #root总在pre的右侧 因此理论上root.val>pre.val
            if pre and root.val<=pre.val:return False
            pre=root
            root=root.right
        return True
```

## java solution
```java
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
    public boolean isValidBST(TreeNode root) {
        return helper(root,Long.MIN_VALUE,Long.MAX_VALUE);
    }
    //利用动态规划 判断每个节点值是否在其应该处于的区间(min,max)
    public boolean helper(TreeNode root,long min,long max)
    {
        if(root==null) return true;
        if(root.val>=max||root.val<=min)return false;
        return helper(root.left,min,root.val)&&helper(root.right,root.val,max);
    }
}
```
