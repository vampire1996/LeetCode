# 16. 3Sum Closest
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/46.Permutations/problem.png"/>

## python solution
```python
class Solution:
    def threeSumClosest(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
       
        
        s=0
        threeSum=sum(nums[0:3])
        closest=abs(sum(nums[0:3])-target)
        l=len(nums)
        if l==3:
          return threeSum
        nums.sort()
        for i in range(l-2):
          if i>0 and nums[i]==nums[i-1]:
              continue
          j=i+1
          k=l-1
          while j<k:
            s=nums[i]+nums[j]+nums[k]
            
            if s-target>0:
               if s-target<closest:
                 closest=s-target
                 threeSum=s
               k-=1
            elif s-target<0:
              if target-s<closest:
                 closest=target-s
                 threeSum=s    
              j+=1
            else:
              threeSum=s
              break
        return threeSum    
```
