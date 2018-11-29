# 94. Binary Tree Inorder Traversal
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/94.%20Binary%20Tree%20Inorder%20Traversal/problem.png"/>

## Morris Traversal
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/94.%20Binary%20Tree%20Inorder%20Traversal/Morris%20Traversal.png"/>

## python solution
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def inorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        """
        思路整理
        1)将根节点的所有左孩子入队
        2)找到最左侧的节点 它没有左孩子 将其弹出加入res
        3)将该节点所有左孩子入队 并找到最左侧的节点 将其弹出加入res
        4）依次重复上述过程直到stack为空
        """
        #Iterative Solution
        stack=[]
        res=[]
        while root:
            stack.append(root)
            root=root.left
        while stack:
            #弹出队尾的元素 先进先出
            node=stack.pop() 
            res.append(node.val)
            root=node.right
            while root:
                stack.append(root)
                root=root.left
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
    def inorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        """
        preorder: root-left-right
        inorder: left-root-right
        postorder: left-right-root
        """
        #Recursive solution
        res=[]
        def helper(res,node):
            if not node:
                return 
            if node.left:
                helper(res,node.left)
            res.append(node.val)
            if node.right:
                helper(res,node.right)    
        helper(res,root)
        return res            
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
    public List<Integer> inorderTraversal(TreeNode root) {
    List<Integer> list = new ArrayList<Integer>();

    Stack<TreeNode> stack = new Stack<TreeNode>();
    TreeNode cur = root;

    while(cur!=null || !stack.empty()){
        while(cur!=null){
            stack.add(cur);
            cur = cur.left;
        }
        cur = stack.pop();
        list.add(cur.val);
        cur = cur.right;
    }

    return list;
}
}
```
