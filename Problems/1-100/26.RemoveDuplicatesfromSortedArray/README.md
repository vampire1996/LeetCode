### 26. Remove Duplicates from Sorted Array
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/26.RemoveDuplicatesfromSortedArray/problem.png "/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/26.RemoveDuplicatesfromSortedArray/clarification.png "/>

## c solution
```c
int removeDuplicates(int* nums, int numsSize) {
    if (numsSize==0) return 0;
    int length=1;
    int j=1;
    for(int i=0;i<numsSize,j<numsSize;i++,j++)
    {
        if(nums[i]==nums[j])
        {
            continue;
        }
        else
        {
            nums[length]=nums[j]; 
            length++;
        }
    }
    return length;
}
```
