# 300. Longest Increasing Subsequence
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/201-300/300.%20Longest%20Increasing%20Subsequence/problem.png"/>

## python solution
```python
class Solution(object):
    def lengthOfLIS(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        """
        思路整理:DP O(n^2)
        Input: [10,9,2,5,3,7,101,18] cur=[1,1,1,2,2,3,4,4]
        1)用cur存储每个位置到该位置时的最大子序列长度
        2)对于每个nums[i] 找到其之前nums中每个小于其的位置j,对应cur[j]+1即为
        从从j到i的长度 而cur[i]需要找到所有这些长度中最大的值
        Explanation
        1)we use cur to store lis in each position in nums
        2)for each nums[i],we need to find all nums[j]<nums[i] and 
        cur[j]+1 is the length form nums[j] to nums[i],and we need to find 
        the longest length among all cur[j]+1 
        """
        if not nums:return 0
        cur=[1 for i in range(len(nums))]
        length=1
        for i in range(1,len(nums)):
            for j in range(i):
                if nums[j]<nums[i]:
                    if cur[j]+1>cur[i]:
                        cur[i]=cur[j]+1
            if cur[i]>length:length=cur[i] 
        return length
```

## java solution
```java
/*
DP O(nlogn)
tails用于存放所有递增子序列的最小值
tails[i] 存放长度为i+1的递增子序列最小值(在nums中)
Input:nums = [4,5,6,3]
len = 1   :      [4], [5], [6], [3]   => tails[0] = 3
len = 2   :      [4, 5], [5, 6]       => tails[1] = 5
len = 3   :      [4, 5, 6]            => tails[2] = 6
利用二分查找
(1)当num>所有tails 则tails.append(num) Size++
(2)当 tails[i-1]<num<=tails[i] tails[i]=num
*/
class Solution {
    public int lengthOfLIS(int[] nums) {
        int[] tails=new int[nums.length];
        int Size=0;
        for(int num:nums)
        {
            int i=0,j=Size;
            while(i<j)
            {
                int m=i+(j-i)/2;
                //最终跳出循环时i=j 因此若tails[m]==num则j=m最终i=j=m
                if(tails[m]<num) i=m+1;
                else j=m;
            }
            tails[i]=num;
            if(i==Size)Size++;
        }
        return Size;
    }
}
```
