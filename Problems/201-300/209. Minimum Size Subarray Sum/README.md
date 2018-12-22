# 209. Minimum Size Subarray Sum
<img src=""/>

## python solution
```python
     
```

## python3 solution
```python3
class Solution:
    def minSubArrayLen(self, s, nums):
        """
        :type s: int
        :type nums: List[int]
        :rtype: int
        """ 
        """
        O(n) solution
        思路整理:
        1)若nums所有元素之和小于s 则不会有邻接的子序列满足sum>=s
        2)用numSum存储nums从第一个元素到第i个元素的和
        3)numSum[end]-numSum[start] 即为从start开始到end 结束的子序列的和
        如果numSum[end]-numSum[start]>=s 则从start到end的序列为满足要求的序列 
        因此start++ 从新的位置开始计算是否符合要求
        否则 end++ 继续扩展当前序列
        Explanation
        1)if the sum of nums is less then s,
        so there is no contiguous subarray of which the sum ≥ s
        2)we use numSum to store the sum from the first element to the ith element
        3)numSum[end]-numSum[start] represents the sum of subarray nums[start:end]
        if numSum[end]-numSum[start]>=s,nums[start:end] satisfies the requirement
        so,start++,we will calculate from a new position
        else end++,expand the current subarray
        """
        if not nums or sum(nums)<s:return 0
        length,l=len(nums),len(nums)
        start,end=0,1
        numSum=[0 for i in range(length+1)]
        for j in range(1,length+1):#O(n)
            numSum[j]=nums[j-1]+numSum[j-1]
        #只有两种情况 end++ 或者start++ 
        #因此当end 和start都为len(nums)也不过是2*len(nums)次循环
        while end<=length and start<end:
            if numSum[end]-numSum[start]>=s:
                if l>end-start:l=end-start
                start+=1
            else:end+=1         
        return l
```


## java solution
```java
class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        if(nums==null||nums.length==0)return 0;
        int start=0,end=0;
        int sum=0,min=Integer.MAX_VALUE;
        while (end<nums.length)
        {
            sum+=nums[end++];
            //注意这里是while 不是if 
            while(sum>=s)
            {
                min=Math.min(min,end-start);
                sum-=nums[start++];
            }
        }
        return (min==Integer.MAX_VALUE)?0:min;
    }
}     
```
