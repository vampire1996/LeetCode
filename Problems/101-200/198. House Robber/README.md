# 198. House Robber
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/198.%20House%20Robber/problem.png "/>

## c solution
```c
int rob(int* nums, int numsSize) {
    if(numsSize==0) return 0;
    if(numsSize==1) return nums[0];
    int *max;//用于存放每个位置可能的rob最大值
    max=malloc(sizeof(int)*numsSize);
    max[0]=nums[0],max[1]=nums[0]>nums[1]?nums[0]:nums[1];
   for(int i=2;i<numsSize;i++)
   {
       max[i]=(nums[i]+max[i-2])>max[i-1]?(nums[i]+max[i-2]):max[i-1];
   }
    return max[numsSize-1]>max[numsSize-2]?max[numsSize-1]:max[numsSize-2];
}
```
