# 101. Symmetric Tree
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

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
bool isNodeSymmetric(struct TreeNode* leftNode,struct TreeNode* rightNode)
{
    if(leftNode==NULL&&rightNode==NULL)   return true;
    if(leftNode==NULL||rightNode==NULL)   return false;
    return (leftNode->val==rightNode->val)&&isNodeSymmetric(leftNode->left,rightNode->right)&&
        isNodeSymmetric(leftNode->right,rightNode->left);
}
bool isSymmetric(struct TreeNode* root) {
    if(root==NULL) return true;
    return isNodeSymmetric(root->left,root->right);   
}

```
