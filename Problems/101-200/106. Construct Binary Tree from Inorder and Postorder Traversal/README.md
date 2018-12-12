# 106. Construct Binary Tree from Inorder and Postorder Traversal
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
    def buildTree(self, inorder,  postorder):
        """
        :type inorder: List[int]
        :type postorder: List[int]
        :rtype: TreeNode
        """
        """
        利用pop()操作 依次从postorder中取出元素因此不需要计算左右子树的范围
        注意要先计算右子树再计算左子树
        """
        if not inorder or not postorder:return None
        node=TreeNode(postorder.pop())
        i=inorder.index(node.val)
        node.right=self.buildTree(inorder[i+1:], postorder)
        node.left=self.buildTree(inorder[:i], postorder)
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
    def buildTree(self, inorder, postorder):
        """
        :type inorder: List[int]
        :type postorder: List[int]
        :rtype: TreeNode
        """
        """
        思路整理:
        1)[lo,hi]代表postorder当前要处理的元素范围 postorder[hi] 为当前函数的根节点
        [start,end]代表inorder当前要处理的元素范围
        在inorder中找到postorder[hi]对应的秩index
        则end-index 为右子树的长度 [hi-(end-index),hi-1]即为postorder中右子树的范围 
        同理[lo,hi-(end-index)-1]即为postorder中左子树的范围
        而[index+1,end]为inorder中右子树的范围 [start,index-1]为inorder中左子树的范围
        e.g.  lo=0  hi=4  start=0  end=4
        inorder = [9,3,15,20,7]     index(postorder[hi])=1   end-index=3
        postorder = [9,15,7,20,3]  node.val=postorder[hi]=3
        则postorder中右子树的范围 [hi-(end-index),hi-1]=[1,3]=[3,15,20]
        postorder中左子树的范围 [lo,hi-(end-index)-1]=[0,0]=[9]
        则inorder中右子树的范围 [index+1,end]=[2,4]=[3,15,20]
        inorder中左子树的范围 [start,index-1]=[0,0]=[9]
        Explanation
        1)[lo,hi]represents the range of elements in postorder 
        postorder[hi] is current root
        [start,end]represents the range of elements in inorder
        thus end-index is the length of right child  
        [hi-(end-index),hi-1] is the range of right child  in postorder 
        [lo,hi-(end-index)-1] is the range of left child  in postorder 
        """
        if not inorder:return None
        def helper(lo,hi,start,end):
            if lo>hi or start>end:return None
            node=TreeNode(postorder[hi])
            index=inorder.index(postorder[hi])
            node.right=helper(hi-(end-index),hi-1,index+1,end)
            node.left=helper(lo,hi-(end-index)-1,start,index-1)
            return node
        return helper(0,len(inorder)-1,0,len(inorder)-1)   
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
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        if(inorder==null||postorder==null)return null;
        HashMap<Integer,Integer> map=new HashMap<Integer,Integer>();
        for(int i=0;i<inorder.length;i++)
        {
            map.put(inorder[i],i);
        }
        return helper(0,inorder.length-1,0,inorder.length-1,map,inorder,postorder);
    }
    private static TreeNode helper(int lo,int hi,int start,int end,HashMap<Integer,Integer> map,int[] inorder, int[] postorder)
    {
        if(lo>hi||start>end) return null;
        TreeNode node=new TreeNode(postorder[hi]);
        int index=map.get(postorder[hi]);
        node.right=helper(hi-(end-index),hi-1,index+1,end,map,inorder,postorder);
        node.left=helper(lo,hi-(end-index)-1,start,index-1,map,inorder,postorder);
        return node;
    }
}
```
