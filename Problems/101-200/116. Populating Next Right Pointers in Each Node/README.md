# 116. Populating Next Right Pointers in Each Node
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## python solution
```python
# Definition for binary tree with next pointer.
# class TreeLinkNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
#         self.next = None
"""
思路整理 BFS+Queue
1)利用队列 存储每一代的节点 
2)对于每一代节点 迭代执行：
    i.node为当前节点 pre为其左侧的节点
    ii.令pre指向node即可 最后一个节点指向空
Explanation
1)use queue to store the node's in one certain generation
2)for each,generation,iteratively conduct:
   i.node is current node and pre is the node in its left side
   ii.let pre points to node and let the last node points to null
"""
class Solution:
    # @param root, a tree link node
    # @return nothing
    def connect(self, root):
        if not root:return
        queue=[root]
        while queue:
            #range(len(queue)) 生成[0,...len(queue)-1]可迭代的列表 
            #不会因为len(queue)改变而改变
            for i in range(len(queue)): 
                node=queue.pop(0)
                if node.left:
                    queue.append(node.left)
                    queue.append(node.right)
                if i>0:pre.next=node
                pre=node
            #下面这句话可加可不加 因为初始化的时候 next就是null
            #pre.next=None
```


## java solution
```java
/**
 * Definition for binary tree with next pointer.
 * public class TreeLinkNode {
 *     int val;
 *     TreeLinkNode left, right, next;
 *     TreeLinkNode(int x) { val = x; }
 * }
 */
public class Solution {
    public void connect(TreeLinkNode root) {
        bfs(root);
    }
    //dfs 0ms  O(n) time complexity O(1) space complexity
    /*
      1 -> NULL                 1 -> NULL                   1 -> NULL
    /  \             --->      /  \         --->           /  \ 
   2    3 -> NULL             2 -> 3 -> NULL              2 -> 3 -> NULL
  / \  / \                   / \  / \                    / \  / \
 4  5  6  7 -> NULL         4  5  6  7 -> NULL          4->5->6  7 -> NULL
 
     1 -> NULL
    /  \             
   2 -> 3 -> NULL             
  / \  / \                  
 4->5->6->7 -> NULL         

    */
    private void dfs(TreeLinkNode root)
    {
        if(root==null)return;
        //把当前节点的左节点指向右节点
        if(root.left!=null)root.left.next=root.right;
        //把当前节点的右节点指向当前节点右节点的左节点
        if(root.right!=null&&root.next!=null)root.right.next=root.next.left;
        dfs(root.left);
        dfs(root.right);
    }
    //bfs 1ms  O(n) time complexity O(1) space complexity
   /*
      1 -> NULL                 1 -> NULL                   1 -> NULL
    /  \             --->      /  \         --->           /  \ 
   2    3 -> NULL             2 -> 3 -> NULL              2 -> 3 -> NULL
  / \  / \                   / \  / \                    / \  / \
 4  5  6  7 -> NULL         4  5  6  7 -> NULL          4->5->6->7 -> NULL             
    */
    private void bfs(TreeLinkNode root)
    {
        if(root==null)return;
        TreeLinkNode cur=root;
        while(root!=null)
       {
            while(cur!=null)
           {
            if(cur.left!=null)cur.left.next=cur.right;
            if(cur.right!=null&&cur.next!=null)cur.right.next=cur.next.left;
            cur=cur.next;
           }
           cur=root.left;
           root=root.left; 
        }
    }
}
```
