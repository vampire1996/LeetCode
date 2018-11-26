# 136. Single Number
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/136.%20Single%20Number/problem.png"/>

## python solution
```python
class Solution(object):
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        """
        Logic: XOR will return 1 only on two different bits. So if two numbers are the same, XOR will return 0. Finally only one number left.
        A ^ A = 0 and A ^ B ^ A = B.
        1 ^ 1 ^ 1 = 1
        1 ^ 0 ^ 1 = 0
        0 ^ 1 ^ 0 = 1
        0 ^ 0 ^ 0 = 1
        """
        #runtime O(n) no extra space
        for i in nums[1:]:
            nums[0]^=i
        return nums[0]    
```

## python3 solution
```python3
class Solution:
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        #超时了
        l=len(nums)
        i,j=0,0
        while i<l:
            j=i+1
            while j<l:
                if nums[i]==nums[j]:
                    temp=nums[i+1]
                    nums[i+1]=nums[j]
                    nums[j]=temp
                    i+=2
                    break
                else:
                    j+=1         
            if j==l:
                return nums[i]  
        return nums[i]
```
