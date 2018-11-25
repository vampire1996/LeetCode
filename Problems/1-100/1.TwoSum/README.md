# 1. Two Sum
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* twoSum(int* nums, int numsSize, int target) {
        int targetNum[numsSize];
        int* newArray=NULL;
        int j=0;
        for(int i=0;i<numsSize;i++)
        {
            targetNum[i]=target-nums[i];
        }
        for(int i=0;i<numsSize;i++)
            for(j=i+1;j<numsSize;j++)
            {
                if(targetNum[i]==nums[j])
                {
                    newArray=(int*)malloc(sizeof(int)*2);
                    newArray[0]=i;
                    newArray[1]=j;
                    break;
                }
            }
       return newArray;
    
}
```

