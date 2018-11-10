# 217. Contains Duplicate
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
bool containsDuplicate(int* nums, int numsSize) {
    if(numsSize==0) return false;
    if(numsSize==1) return false;
    if(nums[0]==nums[1]) return true;
    int maxNum=nums[0],minNum=nums[0];
    for(int i=1;i<numsSize;i++)
    {
        maxNum=maxNum>nums[i]?maxNum:nums[i];
        minNum=minNum<nums[i]?minNum:nums[i];
    }
    int *hash=malloc(sizeof(int)*(maxNum-minNum+1));
    memset(hash,-1,(maxNum-minNum+1)*sizeof(int));
    for(int i=0;i<numsSize;i++)
    {
        hash[nums[i]-minNum]++;
        if( hash[nums[i]- minNum]==1) return true;
    }
    return false;
}
/*
int comp (const void * a, const void * b) {
   return ( *(int*)a - *(int*)b );//a-b代表升序排列
}


bool containsDuplicate(int* nums, int numsSize) {
    // Sort
    qsort(nums, numsSize, sizeof(int), comp);
    //参数： 1 待排序数组首地址
    //2 数组中待排序元素数量
    //3 各元素的占用空间大小
    //4 指向函数的指针，用于确定排序的顺序
    
    // Loop
    for (int i = 0; i < numsSize - 1; i++) {
        if (nums[i] == nums[i+1]) return true;
    }
    
    return false;
}*/
```
