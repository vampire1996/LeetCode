# 15. 3Sum
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/15.%203Sum/problem.png"/>


## python solution
```python
class Solution(object):
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        """
        The idea is to sort an input array and then run through all indices of a possible first 
        element of a triplet. For each possible first element we make a standard bi-directional 2Sum 
        sweep of the remaining part of the array. Also we want to skip equal elements to avoid
        duplicates in the answer without making a set or smth like that.
        """
        l=len(nums)
        nums.sort()
        if l<3 or nums[0]>0 or nums[l-1]<0:
            return []
        res=[]
        for i in range(l-2):
            #nums[i]!=nums[i-1]表明之前用过的重复元素不再使用 
            if i==0 or (i>0 and nums[i]!=nums[i-1]):
                target=0-nums[i]
                lo,hi=i+1,l-1
                while lo<hi:
                    if nums[lo]+nums[hi]==target:
                        res.append([nums[i],nums[lo],nums[hi]])
                        while lo<hi and nums[lo]==nums[lo+1]:lo+=1
                        while lo<hi and nums[hi]==nums[hi-1]:hi-=1
                        lo+=1
                        hi-=1
                    elif nums[lo]+nums[hi]>target:hi-=1
                    else:lo+=1
        return res   
```

## python3 solution
```python3
class Solution:
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        #超时了
        l=len(nums)
        nums.sort()
        if l<3 or nums[0]>0 or nums[l-1]<0:
                 return []
        res=[]
        def helper(lo,hi):   
            if hi-lo+1<3 or nums[lo]>0 or nums[hi]<0:
                 return
            twoSum=nums[lo]+nums[hi]
            
            if twoSum<0:
                k=hi-1
                while k>lo:
                    if nums[k]+twoSum==0:
                        res.append([nums[lo],nums[k],nums[hi]])
                        return True
                        break
                    elif nums[k]+twoSum>0: 
                            k-=1
                    else:break
            else:
                k=lo+1
                while k<hi:
                    if nums[k]+twoSum==0:
                        res.append([nums[lo],nums[k],nums[hi]])
                        return True
                        break
                    elif nums[k]+twoSum<0: 
                            k+=1
                    else:break
           
            return False    
        lo,hi=0,l-1   
        while lo<l-2:
            hi=l-1
            while lo<hi-1:
                 if helper(lo,hi):
                        while lo<hi and nums[hi]==nums[hi-1]:
                              hi-=1
                 hi-=1   
            while lo<l-1 and nums[lo]==nums[lo+1]:
                  lo+=1       
            lo=lo+1
        return res     
```
