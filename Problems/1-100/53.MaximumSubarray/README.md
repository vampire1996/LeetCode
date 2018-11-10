# 53. Maximum Subarray
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/53.MaximumSubarray/problem.png "/>

## c solution
```c
int findmax(int a,int b)
{
    return a>b?a:b;
}
int maxSubArray(int* nums, int numsSize) {
    int maxSum=nums[0];
    int sum=0;
    for(int i=0;i<numsSize;i++)
    {
        sum+=nums[i];
        maxSum=findmax(sum,maxSum);//之前的最大值与加上一个数后作比较得到新的最大值
        sum=findmax(sum,0);//加上一个新的数之后的最大值
    }
    return maxSum;
}
```
