# 2. Add Two Numbers
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2) {
    struct ListNode* head,* tail,* node;
    head = (struct ListNode*)malloc(sizeof(struct ListNode));//分配地址
    tail=head;
    tail->next=NULL;
    int carry=0,sum=0;
    sum=l1->val+l2->val+carry;
    tail->val=sum%10;
    carry=sum/10;
    l1=l1->next;
    l2=l2->next;
    while(l1||l2||carry==1)
    {
        node = (struct ListNode*)malloc(sizeof(struct ListNode));//分配地址
        tail->next=node;
        tail=node;
        tail->next=NULL;//注意要将next指向空
        if(l1&&l2)
        {
            sum=l1->val+l2->val+carry;
            node->val=sum%10;
            carry=sum/10;
            l1=l1->next;
            l2=l2->next;
        }
        else if(l1)
        {
            sum=l1->val+carry;
            node->val=sum%10;
            carry=sum/10;
            l1=l1->next;
        }
        else if(l2)
        {
            sum=l2->val+carry;
            node->val=sum%10;
            carry=sum/10;
            l2=l2->next;
        }
        else if(carry==1)
        {
            node->val=1;
            carry=0;
        }
    }  
    return head;
}
```
