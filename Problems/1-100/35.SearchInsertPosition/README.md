# 35. Search Insert Position
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
int searchInsert(int* nums, int numsSize, int target) {
    int i;
    for(i=0;i<numsSize;i++)
    {
        if(target>nums[i])
            continue;
        else return i;
    }
    return i;
}
```
