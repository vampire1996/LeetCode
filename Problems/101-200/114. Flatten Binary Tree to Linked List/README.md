# 114. Flatten Binary Tree to Linked List
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/114.%20Flatten%20Binary%20Tree%20to%20Linked%20List/problem.png"/>

## python solution
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def flatten(self, root):
        """
        :type root: TreeNode
        :rtype: void Do not return anything, modify root in-place instead.
        """
        """
        思路整理
        1)利用morris traversal对二叉树进行先序遍历 root-left-right
        2)从中序遍历得到的数组中一次取数，由上到下连接成题目要求的 flattened tree(扁平的树)
        Explanation
        1)use morris taversal to get an array which is obtained by the inorder traversal 
        of one given tree
        2)take the elements from res and link the tree node respectively
        """
        
        if not root:return
        stack=[root]
        res=[root]
        node=root
        while stack:
            while node and node.left:
                res.append(node.left)
                stack.append(node.left)
                node=node.left
            node=stack.pop()#默认删除列表最后一个元素
            if node.right:
                res.append(node.right)
                stack.append(node.right)
            node=node.right
        node=root
        a=res.pop(0)
        while res:
            node.right=res.pop(0)
            node.left=None
            node=node.right
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
    prev=None
    def flatten(self, root):
        """
        :type root: TreeNode
        :rtype: void Do not return anything, modify root in-place instead.
        """
        """
        Input:
            1
           / \
          2   5
         / \   \
        3   4   6
        思路整理:postorder left-right-root这里用right-left-root
        对于   2   首先当root=4 prev=4之后root=3 root.right=4 root.left=None-->  2
              /\                                                               /
             3  4                                                             3
                                                                               \
                                                                                4
            之后当root=2 prev=3  root.right=3 root.left=None       -->  2
                                                                        \
                                                                         3
                                                                          \
                                                                           4
        按照此思路递归即可
        """
        if not root:return
        self.flatten(root.right)
        self.flatten(root.left)
        root.right=self.prev
        root.left=None
        self.prev=root
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
思路:
对于root       -->      root  首先交换left，right  再访问right(原left)的最右一个元素it  令it.right=root.left(原right)即可
   /    \                 \
 left   right             left
                           \
                           right
*/
class Solution {
    public void flatten(TreeNode root) {
        TreeNode temp=new TreeNode(0);
        TreeNode it=new TreeNode(0);       
        for(TreeNode a=root;root!=null;root=root.right)
        {
            if(root.right==null)
            {
                root.right=root.left;
                root.left=null;
            }
            else if(root.left!=null)
            {
                System.out.printf("%d",root.val);
                temp=root.right;
                root.right=root.left;
                root.left=temp;
                for(it=root;it.right!=null;it=it.right);
                temp=it.right;
                it.right=root.left;
                root.left=temp;
            }
        }
    }
}
```
