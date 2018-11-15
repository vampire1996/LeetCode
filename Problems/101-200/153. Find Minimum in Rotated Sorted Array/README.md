# 153. Find Minimum in Rotated Sorted Array
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/153.%20Find%20Minimum%20in%20Rotated%20Sorted%20Array/problem.png"/>


## python solution
```python
class Solution:
    def findMin(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        
        l=len(nums)
        if l==1:
            return nums[0]
        Min=nums[0]
        for i in range(0,l-1):
          if nums[i]>nums[i+1]:
            Min=nums[i+1]
            break
            
        return Min   
```
