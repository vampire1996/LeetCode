# 33. Search in Rotated Sorted Array
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/2.AddTwoNumbers/problem.png"/>

## python solution
```python
class Solution(object):
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        """
        考虑两种情况:
        1.234567891旋转的后缀长于未旋转的前缀
        1)target>nums[mi] 7,8,9
        lo=mi-1
        2)target<nums[mi] 
        i.target>nums[hi] 2,3,4
        hi=mi-1
        ii.target<=nums[hi] 1
        lo=mi+1
        2.912345678旋转的后缀短于未旋转的前缀
        1)target>nums[mi] 
        i.target<nums[lo] 5,6,7,8
        lo=mi+1
        ii.target>=nums[lo] 9
        hi=mi-1
        2)target<nums[mi]  1,2,3
        hi=mi-1
        """
        if not nums:return -1
        l=len(nums)
        lo,hi=0,l-1
        while lo<hi:
            mid=int((lo+hi)/2)
            if nums[mid]==target:return mid
            elif target<nums[mid]:
                if nums[mid]>nums[hi] and target<=nums[hi]:
                    lo=mid+1
                else:hi=mid-1
            else:
                if nums[mid]<nums[lo] and target>=nums[lo]:
                    hi=mid-1
                else:lo=mid+1
        if nums[lo]==target:return lo
        return -1
```

## python3 solution
```python3
class Solution:
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        """
        Input:[4,5,6,7,0,1,2]
        how to solve:
        find the smallest element in nums and its index is lo nums[4]=0
        if target is larger than nums[l-1]=2 use binary search among nums[0:lo]--4,5,6,7
        else use binary search among nums[lo:l-1]--0,1,2
        """
        if not nums:return -1
        def binarySearch(lo,hi,x):
            if x>nums[hi] or x<nums[lo]: return -1
            if lo==hi: return lo
            while lo<hi:
                mid=int((lo+hi)/2) 
                if nums[mid]==x:return mid
                elif nums[mid]>x:hi=mid-1
                else:lo=mid+1        
            if nums[lo]==target:return lo
            return -1
        l=len(nums)
        lo,hi=0,l-1
        while lo<hi:
            mi=int((lo+hi)/2)
            if nums[mi]>nums[hi]:lo=mi+1
            else:hi=mi
        if target>nums[l-1]:return binarySearch(0,lo-1,target)
        else:return binarySearch(lo,l-1,target)
        return -1
```

java solution
```java
/*Explanation
Let's say nums looks like this: [12, 13, 14, 15, 16, 17, 18, 19, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
Because it's not fully sorted, we can't do normal binary search. But here comes the trick:

If target is let's say 14, then we adjust nums to this, where "inf" means infinity:
[12, 13, 14, 15, 16, 17, 18, 19, inf, inf, inf, inf, inf, inf, inf, inf, inf, inf, inf, inf]

If target is let's say 7, then we adjust nums to this:
[-inf, -inf, -inf, -inf, -inf, -inf, -inf, -inf, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
And then we can simply do ordinary binary search.
*/
class Solution {
    public int search(int[] nums, int target) {
        //length--针对数组 length()--针对字符串
        //这种lo和hi的取法针对nums[0:length)的情况 右边取不到
        int lo=0,hi=nums.length;
        while (lo<hi)
        {
            int mi=(lo+hi)/2;
            //If nums[mid] and target are "on the same side" of nums[0], we just take nums[mid].
            //Otherwise we use Integer.MIN_VALUE or Integer.MAX_VALUE as needed.
            int num=(target<nums[0])==(nums[mi]<nums[0])?
                nums[mi]:(nums[mi]<nums[0])?Integer.MAX_VALUE:Integer.MIN_VALUE;
            if(num==target)return mi;
            else if (num>target) hi=mi;
            else lo=mi+1;
        }
        return -1;
    }
}
```
