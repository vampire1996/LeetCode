# 100. Same Tree
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/100.%20Same%20Tree/problem.png "/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/100.%20Same%20Tree/example.png "/>

## c solution
```c
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;// node data 
 *     struct TreeNode *left; //pointer to left subtree 
       //正确的 指针的长度是确定的
      //struct TreeNode left;//错误的  在分配内存的时候，由于无限嵌套，也无法确定这个结构体的长度，所以这种方式是非法的。
 *     struct TreeNode *right;//pointer to right subtree
 * };
 例：
  struct Person{

        char *name;

        int age;

        //嵌套自己类型的指针

        struct Person *child;
  };
    struct Person kim = {"kim",8,NULL};
    struct Person p1 = {"林志颖",35,&kim};
    //结构体嵌套自身指针的，访问
    printf("%s的儿子是:%s,儿子的年龄:%d\n",p1.name,(*p1.child).name,(*p1.child).age);
    printf("%s的儿子是:%s,儿子的年龄:%d\n",p1.name,p1.child->name,p1.child->age); 
 */
/*bool isSameTree(struct TreeNode* p, struct TreeNode* q) ;
int main ()
{
    struct TreeNode a={1,NULL,NULL};
    struct TreeNode b={2,NULL,NULL};
    struct TreeNode c={2,&a,&b};
    struct TreeNode d={1,NULL,NULL};
    struct TreeNode e={2,NULL,NULL};
    struct TreeNode f={2,&d,&e};
    isSameTree(&c,&f);
    return 0;
}*///leetcode 的main函数被隐藏了 所以不能自己写main函数

bool isSameTree(struct TreeNode *p,struct TreeNode *q)
{
    if(p==NULL&&q==NULL)
        return true;
    if(p==NULL&&q!=NULL)
        return false;
    if(p!=NULL&&q==NULL)
        return false;
    if(p->val!=q->val)
    return false;
    return isSameTree(p->left,q->left)&&isSameTree(p->right,q->right);
}
```
