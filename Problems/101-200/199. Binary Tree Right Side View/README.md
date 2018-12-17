# 199. Binary Tree Right Side View
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/199.%20Binary%20Tree%20Right%20Side%20View/problem.png"/>

## python solution
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def rightSideView(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        """
        思路整理
        1)对二叉树进行先序遍历(root--left--right)
        2)将每一层的最后一个元素加到res队尾
        explanation
        1)take the preorder trversal for the binary tree
        2)add the last element to res in stack
        Input:
          1            stack=[1]    res=[1]
        /   \
       2     3         stack=[2,3]  res=[1,3]
        \     \
         5     4       stack=[5,4]  res=[1,3,4]
        """
        if not root:return []
        stack=[root]
        res=[root.val]
        while stack:
            k=len(stack)
            for i in range(k):
                #pop() 函数用于移除列表中的一个元素（默认最后一个元素）
                node=stack.pop(0)#移除列表中的第一个元素
                if node.left:stack.append(node.left)
                if node.right:stack.append(node.right)
            if stack:
                res.append(stack[-1].val)
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
/*
1.Each depth of the tree only select one node.
2. View depth is current size of result list.
*/
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        //Vector主要用在事先不知道数组的大小，或者只是需要一个可以改变大小的数组的情况。 
        //创建一个默认的向量，默认大小为10：
        ArrayList res = new ArrayList<Integer>();
        helper(res,root,0);
        return res;
    }
    //DFS-traverse the tree right-to-left, add values to the res whenever we first reach a new record depth.
    //当depth第一次增加1 即到达下一层时 添加最右边的元素到res
    public void helper(ArrayList res,TreeNode node,int depth)
    {
        if(node!=null)
        {
            // size()是集合的方法,可以返回集合中对象的数量 length()是数组的方法,返回数组的长度
            if(res.size()==depth)
            {
                res.add(new Integer(node.val));
            }
            helper(res,node.right,depth+1);
            helper(res,node.left,depth+1);
        }
    }
}
```
