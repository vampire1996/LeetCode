# 104. Maximum Depth of Binary Tree
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/104.MaximumDepthofBinaryTree/problem.png "/>

## c solution
```c
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */
/*其他方案
int maxDepth(struct TreeNode *root) {
	if(NULL==root) return 0;
    
	int l_d=maxDepth(root->left);
	int r_d=maxDepth(root->right);

	return l_d>r_d? l_d+1 : r_d+1;
}*/
int nodeMaxDepth(struct TreeNode* leftNode,struct TreeNode* rightNode,int depth)
{
    if(leftNode==NULL&&rightNode==NULL)   return  depth;
    if(leftNode!=NULL&&rightNode==NULL)   
    {
        
        return  nodeMaxDepth(leftNode->left,leftNode->right,depth+1);
    }
    if(leftNode==NULL&&rightNode!=NULL)   
    {
        return  nodeMaxDepth(rightNode->left,rightNode->right,depth+1);
    }
    int leftDepth=nodeMaxDepth(leftNode->left,leftNode->right,depth+1);   
    int rightDepth=nodeMaxDepth(rightNode->left,rightNode->right,depth+1); 
    return  leftDepth>rightDepth?leftDepth:rightDepth;
}
int maxDepth(struct TreeNode* root) {
    if(root==NULL) return 0;
    return nodeMaxDepth(root->left,root->right,1);  
}
```
