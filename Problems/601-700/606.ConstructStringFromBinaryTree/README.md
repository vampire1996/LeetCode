# 606. Construct String from Binary Tree
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
char* tree2str(struct TreeNode* t) {
  if(t==NULL) return "";
    char* s;
  if(t->left==NULL&&t->right==NULL)
  {
      s=malloc(sizeof(char)*5);
      sprintf(s,"%d",t->val);//sprintf 将t->val格式化后置于字符数组s中
  }
  else if (t->left!=NULL&&t->right==NULL)
  {
      char *leftS=tree2str(t->left);
      s=malloc(sizeof(char)*(10+strlen(leftS)));
      sprintf(s,"%d(%s)",t->val,leftS);
  }
  else if(t->left==NULL&&t->right!=NULL)
  {
      char *rightS=tree2str(t->right);
      s=malloc(sizeof(char)*(10+strlen(rightS)));
      sprintf(s,"%d()(%s)",t->val,rightS);
  }
  else if(t->left!=NULL&&t->right!=NULL)
  {
      char *leftS=tree2str(t->left);
      char *rightS=tree2str(t->right);
      s=malloc(sizeof(char)*(10+strlen(leftS)+strlen(rightS)));
      sprintf(s,"%d(%s)(%s)",t->val,leftS,rightS);
  }          
  return s;
}
```
