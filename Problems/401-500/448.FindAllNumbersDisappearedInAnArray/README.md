# 448. Find All Numbers Disappeared in an Array
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
/**
 * Return an array of size *returnSize.
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* findDisappearedNumbers(int* nums, int numsSize, int* returnSize) {
    int *a=malloc(sizeof(int)*numsSize+1);
    int j=0;
    memset(a,0,sizeof(int)*numsSize);
    for(int i=0;i<numsSize;i++) a[nums[i]-1]++;
    for(int i=0;i<numsSize;i++)
    {
       if (a[i]==0) a[j++]=i+1;     
        else a[i]=NULL;
    }
    * returnSize=j;
    return a;
}
```
