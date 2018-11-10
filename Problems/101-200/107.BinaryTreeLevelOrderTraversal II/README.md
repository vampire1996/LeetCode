# 107. Binary Tree Level Order Traversal II
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
/**
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *columnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */
int TreeDepth(struct TreeNode* root)//计算树的深度
{
    if(!root) return 0;
    int left=TreeDepth(root->left);
    int right=TreeDepth(root->right);
    if( left>right)
        return left+1;
    else 
        return right+1;
    
}
int** levelOrderBottom(struct TreeNode* root, int** columnSizes, int* returnSize) {
    if(!root) return NULL;
   int depth=*returnSize=TreeDepth(root);
   int** returnArray = (int**)malloc(depth*sizeof(int*)); 
    *columnSizes = (int*)malloc(depth*sizeof(int));
   struct TreeNode* root_history[10000];
   int front=0,rear=0;
   root_history[rear++]=root; 
    while(rear>front)
    {
        int end=rear,start=front;
         (*columnSizes)[--depth] = end - start;
        returnArray[depth]=(int*)malloc(sizeof(int)*(end-start));
        front=end;
        for(int i=start;i<end;i++)
        {
          returnArray[depth][i-start]= root_history[i]->val;
          if(root_history[i]->left) root_history[rear++]=root_history[i]->left;
          if(root_history[i]->right) root_history[rear++]=root_history[i]->right;
        }
        
    }
    return returnArray;
}
```
