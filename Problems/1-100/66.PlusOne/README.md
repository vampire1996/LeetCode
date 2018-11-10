# 66. Plus One
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/66.PlusOne/problem.png "/>

## c solution
```c
/**
 * Return an array of size *returnSize.
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* plusOne(int* digits, int digitsSize, int* returnSize) {
    int i=digitsSize-1;
    int *newDigits=NULL;
    if(!digits|digitsSize<1)
        return NULL;
    while(i>=0)
    {
        if(digits[i]==9)
        {
            digits[i]=0;
            i--;
        
        }
        else
        {
           digits[i]=digits[i]+1;
           break;
        }    
    }    
    if(digits[0]==0)
    {
        *returnSize=digitsSize+1;
        newDigits=(int*)malloc(sizeof(int)*(*returnSize));
        memcpy(newDigits+1,digits,sizeof(int)*digitsSize);
        newDigits[0]=1;
    }
    else
    {
        *returnSize=digitsSize;
        newDigits=(int*)malloc(sizeof(int)*(*returnSize));
        memcpy(newDigits,digits,sizeof(int)*digitsSize);
        
    }
    return newDigits;
}
```
