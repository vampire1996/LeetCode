# 55. Jump Game
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
bool canJump(int* nums, int numsSize) {
    int lo=numsSize-1;
    for(int i=lo;i>=0;i--)
    {
        if(nums[i]>=lo-i) lo=i;
    }
    return lo==0;
}
```

## pyhton solution
```python
class Solution:
    def canJump(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        l=len(nums)
        if l==1:
            return True 
        if l==2:
            return nums[0]>0
        if nums[0]==0:
            return False
        cur=1
        last=0
        temp=cur+nums[cur]
        index=cur
        while cur<l-1:
         if last+nums[last]>=l-1:
            return True  
         if cur-last<=nums[last]:
              if cur+nums[cur]>=l-1 :
                 return True  
              if cur+nums[cur]>=temp:
                 temp=cur+nums[cur]
                 index=cur
              cur+=1
         else :
              last=index
              cur=last+1        
         if nums[last]==0:
            return False
        
        return False
```
