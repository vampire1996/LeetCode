# 485. Max Consecutive Ones
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/401-500/485.MaxConsecutiveOnes/problem.png"/>

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
