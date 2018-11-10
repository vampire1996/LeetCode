# 219. Contains Duplicate II
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/201-300/219.ContainsDuplicate%20II/problem.png "/>

## c solution
```c
/*bool containsNearbyDuplicate(int* nums, int numsSize, int k) {
    int i=0,j=numsSize-1,h=0;
    while(i<numsSize-1)
    {
        while(i<j)
      {
           if(nums[i]==nums[j])
           {
            if((j-i)<=k) return true;
            else
            {
                
                j--;
            }
           }
            else
            {
                
                j--;
            }
      }
      i++;
      j=numsSize-1;  
    }
    return false;
}*/
//使用hash
bool containsNearbyDuplicate(int* nums, int numsSize, int k) {
    if(numsSize ==0) return false;
    if(k>numsSize) k= k% numsSize;
    int i, min= INT_MAX, max = INT_MIN;
    for(i=0; i<numsSize; i++){
        min = min< nums[i]? min: nums[i];
        max = max> nums[i]? max: nums[i];
    }
    int *hash = malloc((max-min+1)* sizeof(int));
    memset(hash, -1, (max-min+1)*sizeof(int));//hash所指向的某一块内存中的后(max-min+1)*sizeof(int)个 字节的内容全部设置为-1
    for(i=0; i<numsSize; i++){
        if(hash[nums[i]-min] == -1){
            hash[nums[i]-min] = i;
        }
        else if((i-hash[nums[i]-min]) <= k){
            return true;
        }
        else{
            hash[nums[i]-min] = i;
        }
    }
    return false;
}
```
