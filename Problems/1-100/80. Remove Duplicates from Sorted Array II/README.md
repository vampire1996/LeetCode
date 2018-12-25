# 80. Remove Duplicates from Sorted Array II
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## python solution
```python
class Solution(object):
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        """
        思路整理
        1)length为要返回的长度 cnt为连续元素相等的子数组长度
        pre为当前元素前一个元素的值
        2)当前元素和pre相等且之前只有一个一个与之相同的元素(pre)
        令nums[length]=nums[i] length代表当前已经符合要求的长度
        因此这句话代表将当前元素赋值给符合要求长度部分的下一个元素
        此时length长度+1
        3)当前元素和pre不等 令nums[length]=nums[i]
        且相应修改pre length cnt的值
        Explanation
        1)lenght represents the length we will return 
        cnt represents the length  of subarray whose elements are 
        constantly equal
        pre represents the previous number before nums[i] 
        2)if nums[i]==pre and cnt==1:#only one number before
        nums[i] equals to nums[i]
        set nums[length]=nums[i],length represents the length
        of the subarray which has arranged according the given 
        requiremnet,after this lenght=length
        3)if nums[i]!=pre
        set nums[length]=nums[i],and change  pre,length,cnt
        """
        if not nums:return
        length,pre,cnt=1,nums[0],1
        for i in range(1,len(nums)):
            if nums[i]==pre and cnt==1:
                nums[length]=nums[i]
                cnt+=1
                length+=1
            elif nums[i]!=pre:
                nums[length]=nums[i]
                pre=nums[i]
                length+=1
                cnt=1
        return length
```

## java solution
```java
class Solution {
    public int removeDuplicates(int[] nums) {
        /*
        nums[i-2]  nums[i-1] nums[i]
           a         a         a
           a         b         b
           a         b         c
           只要nums[i]>nums[i-2] nums[i]即为符合题目要求的元素
           需要加到符合当前要求序列的末端
           然鹅这里nums[i-2]可能已经别修改过了
           Given nums = [1,1,1,2,2,3]
           到nums[4]的时候 nums = [1,1,2,2,2,3]
           所以应该改为nums[length-2]  nums[length-1] nums[i],原理同上
        */
        int length=0;
        for(int num:nums)
        {
            if(length<2||num>nums[length-2])
            {
                nums[length++]=num;
            }
        }
        return length;
    }
}
```
