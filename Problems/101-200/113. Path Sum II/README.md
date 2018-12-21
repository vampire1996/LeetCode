# 113. Path Sum II
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/139.%20Word%20Break/problem.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/139.%20Word%20Break/example.png"/>

## python solution
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

"""
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \    / \
7    2  5   1
BFS+queue
queue是先进先出 因此遍历顺序是5-4-8-11-13-4-7-2-5-1  BFS
"""
class Solution(object):
    def pathSum(self, root, sum):
        if not root:return []
        queue=[(root,[root.val],sum-root.val)]
        res=[]
        while queue:
            cur,path,num=queue.pop(0)#弹出第一个元素
            if not cur.right and not cur.left and num==0:
                res.append(path)
            if cur.left:
                queue.append((cur.left,path+[cur.left.val],num-cur.left.val))
            if cur.right:
                queue.append((cur.right,path+[cur.right.val],num-cur.right.val))
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
    def pathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: List[List[int]]
        """
        """
        思路整理:DFS recursion
        1)用path缓存路径，用num保存路径和
        如果当前节点为叶子结点 且路径和为sum 则在res中加入path
        Explanation
        we use to cache pat,num to store the sum of path
        if current node is a leaf and num==sum,just add path to res
        """
        def helper(res,path,node,num):
            if not node:return 
            if node.left==None and node.right==None:
                if num+node.val==sum:res.append(path+[node.val])
                return
            helper(res,path+[node.val],node.left,num+node.val)
            helper(res,path+[node.val],node.right,num+node.val)
        res=[]
        helper(res,[],root,0)
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
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \    / \
7    2  5   1
DFS 
由于stack是后进先出 
访问次序是5-4-11-7-2-8-13-4-5-1
*/
class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<List<Integer>> res=new ArrayList<>();
        if(root==null)return res;
        Stack<TreeNode> node=new Stack<TreeNode>();
        Stack<List<Integer>> path=new Stack<List<Integer>>();
        Stack<Integer> num=new Stack<Integer>();
        List<Integer> list=new ArrayList<Integer>();
        list.add(root.val);
        node.add(root);
        path.add(list);
        num.add(sum-root.val);
        //push 加到stack头部(top)  add加到stack尾部(end)
        while(!node.isEmpty())
        {
            TreeNode cur=node.pop();
            list=path.pop();
            int curNum=num.pop();
            if(cur.left==null&&cur.right==null&&curNum==0)
            {
                res.add(new ArrayList<>(list));
            }
            
            if(cur.right!=null)
            {
                list.add(cur.right.val);
                node.add(cur.right);
                path.add(new ArrayList<>(list));
                num.add(curNum-cur.right.val);
                list.remove(list.size()-1);
            }
            if(cur.left!=null)
            {
                list.add(cur.left.val);
                node.add(cur.left);
                path.add(new ArrayList<>(list));
                num.add(curNum-cur.left.val);
                list.remove(list.size()-1);
            }
            
        }
        return res;
    }
}
```
