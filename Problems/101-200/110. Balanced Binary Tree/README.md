# 110. Balanced Binary Tree
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/74.%20Search%20a%202D%20Matrix/problem.png"/>

## python solution
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def isBalanced(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """ 
        """
        思路整理:
        DFS 计算每个节点的深度 如果左右子树深度之差大于1 则该树不是BBT
        返回-1 只要出现一次-1 则最终返回-1 
        否则返回树的深度
        Explanation
        calculate each node's depth if the absolate difference is bigger 
        than 1,we just return -1,when there are one -1 returned,
        we can draw the conclusion that this tree is not a BBT
        """
        def helper(node,depth):
            if not node:return depth
            leftdepth=helper(node.left,depth+1)
            rightdepth=helper(node.right,depth+1)
            if leftdepth==-1 or rightdepth==-1:return -1
            if abs(leftdepth-rightdepth)>1:return -1
            return max(leftdepth,rightdepth)
        return True if helper(root,0)!=-1 else False
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
//用ans作为出现不平衡情况的标志位 只要ans=false则不是BBT
class Solution {
    public boolean isBalanced(TreeNode root) {
        helper(root);
        return ans;
    }
    //private--访问权限仅限于类的内部
    private boolean ans=true;
    private int helper(TreeNode root)
    {
        if(root==null)return 0;
        int left=helper(root.left);
        int right=helper(root.right);
        if(Math.abs(left-right)>1) ans=false;
        return Math.max(left,right)+1;
    }
}
```
