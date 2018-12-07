# 112. Path Sum
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/112.%20Path%20Sum/problem.png"/>

## python solution
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def hasPathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: bool
        """
        if not root:return False
        def helper(node,num):
            if not node.left and not node.right:
                if num+node.val==sum:return True
                else:return
            if node.left:
                if helper(node.left,num+node.val)==True: return True
            if node.right:
                if helper(node.right,num+node.val)==True: return True
        if helper(root,0)==True:return True
        else:return False
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
    def hasPathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: bool
        """
        """
        DFS recursive
        所有从树根到叶子的计算结果进行或运算，只要有一个为真则最终结果为真
        if one of the results of sum from the root to one leaf is true,
        the final result is true,which is what logic 'or' does.
        """
        if not root:return False
        sum-=root.val
        if not root.left and  not root.right:return sum==0
        return self.hasPathSum(root.left,sum) or self.hasPathSum(root.right,sum)
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
/*
A：根节点、B：左节点、C：右节点，
对于本题来说BCA或者CBA都是正确的
前序顺序是ABC  中序顺序是BAC  后序顺序是BCA
stack--后进先出
每个叶子结点的值修改为从树根到该叶子结点的总和
*/
//DFS iterative+postorder traversal
class Solution {
    public boolean hasPathSum(TreeNode root, int sum) {
        if (root==null)return false;
        Stack<TreeNode> node=new Stack<TreeNode>();
        TreeNode curNode=new TreeNode(0);
        int curSum=0;
        node.push(root); 
        while(!node.isEmpty())
        {
            curNode=node.pop();
            curSum=curNode.val;
            if(curNode.left==null&&curNode.right==null)
            {
                if(curNode.val==sum)return true;
            }
            if(curNode.right!=null)
            { 
                curNode.right.val=curSum+curNode.right.val;
                node.push(curNode.right);   
            }
            if(curNode.left!=null)
            {
                curNode.left.val=curSum+curNode.left.val;
                node.push(curNode.left);
            }
        }
        return false;
    }
}
```
