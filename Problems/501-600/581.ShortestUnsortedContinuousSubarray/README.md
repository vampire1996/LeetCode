# 581. Shortest Unsorted Continuous Subarray
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/501-600/581.ShortestUnsortedContinuousSubarray/problem.png"/>

## c solution
```c
int comp(const void*a,const void*b)
{
return *(int*)a-*(int*)b;//a-b是从小到大排序  b-a是从大到小排序
}
int findUnsortedSubarray(int* nums, int numsSize) {
    int Max=INT_MIN,Min=INT_MIN;
    int IndexMin=0,IndexMax=0;
    int *nums2=malloc(sizeof(int)*numsSize+1);
    nums2[numsSize]=NULL;
    for(int i=0;i<numsSize;i++)
    {
      nums2[i]=nums[i];  
    }
    qsort(nums,numsSize,sizeof(int),comp);
    for(int i=0;i<numsSize;i++)
    {
      if(nums[i]<nums2[i]) 
      {
          IndexMin=i;
          break;
      }
    }
    for(int i=numsSize-1;i>=0;i--)
    {
      if(nums[i]>nums2[i]) 
      {
          IndexMax=i;
          break;
      }
    }
    if(IndexMax!=0||IndexMin!=0)
    return IndexMax- IndexMin+1;
    else return 0;
}
```
