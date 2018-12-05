# 95. Unique Binary Search Trees II
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/95.%20Unique%20Binary%20Search%20Trees%20II/problem.png"/>

## python solution
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def generateTrees(self, n):
        """
        :type n: int
        :rtype: List[TreeNode]
        """
        """
        思路整理:
        1) helper的功能是将[lo,hi]的自然数组成一个BST
        2)lo==hi 只有一个数，因此返回由该树节点构成的列表
        3)lo<hi 遍历[lo,hi]的自然数
        [lo,i-1]--左子树  i--树根  [i+1,hi]--右子树
        Explanation
        1)function helper helps us to build a BST using natural number between [lo,hi]
        2)if lo==hi,just return the list which only have one treenode who's value is lo
        2)if lo<hi,traverse the natural numbers between [lo,hi]
        [lo,i-1]--left child  i--树根  [i+1,hi]--right child
        """
        def helper(lo,hi):
            if hi-lo<0:return [None]
            if hi-lo==0:return [TreeNode(lo)]
            res=[]
            for i in range(lo,hi+1):
                leftTrees=helper(lo,i-1)
                rightTrees=helper(i+1,hi)
                for left in leftTrees:
                    for right in rightTrees:
                        root=TreeNode(i)
                        root.left=left
                        root.right=right
                        res.append(root)
            return res
        if n==0:return []
        return helper(1,n)
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
//result[i] stores the result until length i. For the result for length i+1, 
//select the root node j from 0 to i, combine the result from left side and right side. 
//Note for the right side we have to clone the nodes as the value will be offsetted by j.
class Solution {
    public List<TreeNode> generateTrees(int n) {
        List<TreeNode>result[]=new List[n+1];
        result[0] = new ArrayList<TreeNode>();
        if(n==0) return result[0];
        result[0].add(null);
        
        for(int len=1;len<=n;len++)
        {
            result[len] = new ArrayList<TreeNode>();
            for(int j=0;j<len;j++)
            {
                for (TreeNode LChild:result[j])
                {
                    for (TreeNode RChild:result[len-j-1])
                    {
                        TreeNode node=new TreeNode(j+1);
                        node.left=LChild;
                        node.right=clone(RChild,j+1);
                        result[len].add(node);
                    }
                }
            }
        }
      
        return result[n];
    }
   
    private static TreeNode clone(TreeNode node,int offset) {
        if(node==null)return null;
        TreeNode temp=new TreeNode(node.val+offset);
        temp.left=clone(node.left,offset);
        temp.right=clone(node.right,offset);
        return temp;
    }
}
···
