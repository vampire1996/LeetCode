# 75. Sort Colors
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/75.%20Sort%20Colors/problem.png"/>


## python solution
```python
class Solution(object):
    def sortColors(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        '''
        O(n) 20ms beat100%
        思路整理
        扫描num 遇到0则将其置于队首(zeros)
                遇到2则将其置于队尾(tail) 
        '''
        l=len(nums)
        head=0
        tail=l-1
        zeros=0
        while head<=tail:
            if nums[head]==0:
                temp=nums[head]
                nums[head]=nums[zeros]
                nums[zeros]=temp
                head+=1
                zeros+=1
            elif nums[head]==1:
                head+=1
            else:
                temp=nums[head]
                nums[head]=nums[tail]
                nums[tail]=temp
                tail-=1 
```
