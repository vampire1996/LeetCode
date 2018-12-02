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
         """
        example:4,6,5,4,3,2,1
        思路整理:
        1)从最后一个元素开始，判断相邻元素是否是逆序(nums[j]>nums[j-1])
        2)找到第一个逆序的元素(4) 与之前比较过的元素(6,5,4,3,2,1)找到比其大的最小元素(5)
        3)二者交换5,6,4,4,3,2,1
        4)将5之后元素排序5,1,2,3,4,4,6
        5)由于交换后当前元素之后的元素为降序排列 因此只需将其颠倒过来即可reverse
      
        How to solve
        1)From last element in the list,find the first element which is bigger than the element before it
        2)find the element within the element compared before,
        find the smallest element which is bigger than the current element
        3)swap these two numbers5,6,4,4,3,2,1
        4)sort the element after current element5,1,2,3,4,4,6
        5)now that the elements after current element are descending,
        we can only use reverse function to sort it
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
class Solution:
    def nextPermutation(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        """
        Find the largest index i such that nums[k] < nums[k + 1]. If no such index exists, the 
        permutation is sorted in descending order, just reverse it to ascending order and we are done. 
        For example, the next permutation
        Reverse the sub-array from nums[k + 1] to nums[nums.size() - 1].
        """
        l=len(nums)
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
        i=l-2
        while i>=0:
            if nums[i+1]>nums[i]:
                break
            i-=1
        print(i)
        if i<0:reverse(0,l-1)
        else:
            k=l-1
            while k>i:
                 if nums[k]>nums[i]:
                    break
                 k-=1
            swap(i,k)
            reverse(i+1,l-1)
```
