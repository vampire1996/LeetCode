# 31. Next Permutation
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/31.%20Next%20Permutation/problem.png"/>

## python solution
```python
class Solution(object):
    def nextPermutation(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        if not nums:return nums
        def reverse(lo,hi):      
            i=lo
            j=hi
            while i<j:
                temp=nums[i]
                nums[i]=nums[j]
                nums[j]=temp
                i+=1
                j-=1
        def swap(a,b):
            temp=nums[a]
            nums[a]=nums[b]
            nums[b]=temp
        l=len(nums)
        j=l-1
        while j>0:
            if nums[j]>nums[j-1]:
                    i=j
                    while i<l:
                        if nums[i]<=nums[j-1]:
                            break
                        i+=1
                    swap(j-1,i-1)
                    nums[j:]=sorted(nums[j:])
                    break
            j-=1
        if j==0:reverse(0,l-1)
            
```

## python3 solution
```python3

```
