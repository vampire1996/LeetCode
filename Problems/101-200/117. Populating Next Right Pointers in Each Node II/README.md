# 117. Populating Next Right Pointers in Each Node II
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/117.%20Populating%20Next%20Right%20Pointers%20in%20Each%20Node%20II/problem.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/117.%20Populating%20Next%20Right%20Pointers%20in%20Each%20Node%20II/example.png"/>

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
            length=len(queue)
            for i in range(length):
                node=queue.pop(0)
                if i!=0:pre.next=node
                if node.left:queue.append(node.left)
                if node.right:queue.append(node.right)
                pre=node
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
//level traversal
public class Solution {
    public void connect(TreeLinkNode root) {
        TreeLinkNode dummy=new TreeLinkNode(0);
        while(root!=null)
        {
            TreeLinkNode cur=dummy;
            System.out.println(root.val);
            while(root!=null)
            {
                if(root.left!=null)
                {
                    cur.next=root.left;
                    cur=cur.next;
                }
                if(root.right!=null)
                {
                    cur.next=root.right;
                    cur=cur.next;
                }
                root=root.next;
            }
            root=dummy.next;
            //dummy.next必需置为null因为到最后一个level必须将dummy.next置为null才能推出循环 root=null
            dummy.next = null;
        }
    }
}
```
