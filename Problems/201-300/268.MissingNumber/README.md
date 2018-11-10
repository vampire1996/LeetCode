# 268. Missing Number
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/201-300/268.MissingNumber/problem.png "/>

## c solution
```c
int missingNumber(int* nums, int numsSize) {
    int *a=malloc(sizeof(int)*(numsSize+1)+1);
    memset(a,0,sizeof(int)*(numsSize+1));
    for (int i=0;i<numsSize;i++)
    {
        a[nums[i]]++;
    }
    for (int i=0;i<numsSize+1;i++)
    {
        if(a[i]==0) return i;
    }
    return 0;
}
```
