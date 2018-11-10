# 485. Max Consecutive Ones
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
int findMaxConsecutiveOnes(int* nums, int numsSize) {
    int num=0;
    int max=0;
    for(int i=0;i<numsSize;i++)
    {
        if(nums[i]==1) num++;
        else 
        {
            if(num>max) max=num;
            num=0;
        }    
    }
    if(num>max) max=num;
    return max;
}
```
