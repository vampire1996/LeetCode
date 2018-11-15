# 153. Find Minimum in Rotated Sorted Array
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/601-700/696.%20Count%20Binary%20Substrings/problem.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/601-700/696.%20Count%20Binary%20Substrings/example.png"/>

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
