# 34. Find First and Last Position of Element in Sorted Array
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/34.%20Find%20First%20and%20Last%20Position%20of%20Element%20in%20Sorted%20Array/problem.png"/>

## python solution
```python
class Solution(object):
    def searchRange(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        if not nums:return [-1,-1]
        lo,hi=0,len(nums)-1
        start,end=-1,-1
        while lo<hi:
            mi=int((lo+hi)/2)
            if nums[mi]<target:lo=mi+1
            else:hi=mi
        if target==nums[lo]:start=lo
        else:return [-1,-1]
        lo,hi=0,len(nums)-1
        """
        [5 7], target = 5
        Now A[mid] = 5, then according to rule 2, we set i = mid. 
        This practically does nothing because i is already equal to mid.
        As a result, the search range is not moved at all!
        The solution is by using a small trick: instead of calculating mid as mid = (i+j)/2, we now do:
        mid = (i+j)/2+1
        Why does this trick work? When we use mid = (i+j)/2, the mid is rounded to the lowest integer. 
        In other words, mid is always biased towards the left. This means we could have i == mid 
        when j - i == mid, but we NEVER have j == mid. So in order to keep the search range moving, 
        you must make sure the new i is set to something different than mid, 
        otherwise we are at the risk that i gets stuck. But for the new j, it is okay if we set it to mid,
        since it was not equal to mid anyways. 
        Our two rules in search of the left boundary happen to satisfy these requirements, 
        so it works perfectly in that situation. Similarly, when we search for the right boundary, 
        we must make sure i won't get stuck when we set the new i to i = mid. 
        The easiest way to achieve this is by making mid biased to the right, i.e. mid = (i+j)/2+1.
        """
        while lo<hi:
            mi=int((lo+hi)/2+1)
            if nums[mi]>target:hi=mi-1 
            else:lo=mi
        if target==nums[lo]:end=lo
        return [start,end]
```

## python3 solution
```python3
class Solution:
    def searchRange(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        """
        思路整理:
        1)首先利用二分法找到target对应在nums中的秩最大的位置end
        i.未命中 end=-1
        ii.命中[5,7,7,8,8,8,10] nums[lo]=nums[5]=8 end=5
        ii.未命中[5,7,7,8,8,10] 但是nums[lo-1]=nums[4]=8 end=4
        2)利用二分法找到target对应在nums中的秩最小的位置start
        i.未命中 start=-1
        ii.命中[5,7,7,8,8,8,10] nums[lo]=nums[3]=8 start=3
        [5,7,7,7,8,8,10] nums[lo]=nums[4]=8 start=4 
        因此只有一种情况
        Explanation
        1)use binary search to find the element in the nums
          which equals to target while it has the biggest index--end
          i.cannot find target end=-1
          ii.find target end=lo
          iii.cannot find target but the element before nums[lo]==target
              thus end=lo-1
        2)use binary search to find the element in the nums
          which equals to target while it has the samllest index--start
          i.cannot find target start=-1
          ii.find target start=lo
        """
        if not nums:return [-1,-1]
        hi,lo=len(nums),0
        end,start=-1,-1
        while hi>lo:
            mi=int((hi+lo)/2)
            #即使命中也不退出 直到找到秩最大的位置 
            if nums[mi]<=target:lo=mi+1
            else:hi=mi  
        #因为当命中时lo=mi+1 命中的元素在下一次迭代中被舍弃 因此可能出现下次迭代未命中则本次命中的index=end
        if lo<len(nums)and nums[lo]==target:end=lo
        if lo-1>=0 and nums[lo-1]==target:end=lo-1
        hi,lo=len(nums),0
        while hi>lo:
            mi=int((hi+lo)/2)
            if nums[mi]<target:lo=mi+1
            #即使命中也不退出 直到找到秩最小的位置 
            else:hi=mi      
        if lo<len(nums)and nums[lo]==target:start=hi
        return [start,end]
```
