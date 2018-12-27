# 213. House Robber II
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## python solution
```python
class Solution(object):
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        """
        O(n) time complexity O(n) space complexity
        思路整理
        1)计算某一位置最大金钱的方法是 max(pre[i-2],pre[i-3])+nums[i]
        pre[i]为本位置可获得的最大金钱,由于不能找与其相邻的位置，因此只能找pre[i-2],pre[i-3]
        2)由于题目中说明第一个和最后一个元素也是相邻的
        所以利用maxMoney1存储从第一个元素开始到倒数第二个元素每个位置可获得最大金钱
        maxMoney2存储从第二个元素开始到最后一个元素每个位置可获得最大金钱
        则max(max(maxMoney1[-1],maxMoney1[-2]),max(maxMoney2[-1],maxMoney2[-2]))
        倒数第三个元素及之前的元素都会被最后两个元素覆盖
        即为总体可获得的最大金钱
        理由:从第一个元素开始的某一条抢劫路径不可能到达最后，所以包含最后元素就不包含第一个元素
        包含第一个元素就不包含最后一个元素
        Explanation
        Input        abcdefgh
        maxMoney1     bcdefgh  to get the maximum in each position
        maxMoney2    abcdefg
        when you start at the beginning of the array,you can just raech the (n-1)th position
        and if you start at the second position,you can reach the last position
        """
        if not nums:return 0
        if len(nums)<=3:return max(nums)
        maxMoney1,maxMoney2=[],[0]
        for i in range(len(nums)):
            if i==0:maxMoney1.append(nums[i])
            elif i==1:
                maxMoney1.append(nums[i])
                maxMoney2.append(nums[i])
            elif i==2:
                maxMoney1.append(nums[i]+nums[i-2])
                maxMoney2.append(nums[i])
            elif i==3 and i!=len(nums)-1:
                if maxMoney1[i-2]>maxMoney1[i-3]:
                    maxMoney1.append(nums[i]+maxMoney1[i-2])   
                else:
                    maxMoney1.append(nums[i]+maxMoney1[i-3])
                maxMoney2.append(nums[i]+nums[i-2])
            elif i<len(nums)-1:
                if maxMoney1[i-2]>maxMoney1[i-3]:
                    maxMoney1.append(nums[i]+maxMoney1[i-2])   
                else:
                    maxMoney1.append(nums[i]+maxMoney1[i-3])
                if maxMoney2[i-2]>maxMoney2[i-3]:
                    maxMoney2.append(nums[i]+maxMoney2[i-2])   
                else:
                    maxMoney2.append(nums[i]+maxMoney2[i-3]) 
            else:
                if maxMoney2[i-2]>maxMoney2[i-3]:
                    maxMoney2.append(nums[i]+maxMoney2[i-2])   
                else:
                    maxMoney2.append(nums[i]+maxMoney2[i-3]) 
        return max(max(maxMoney1[-1],maxMoney1[-2]),max(maxMoney2[-1],maxMoney2[-2]))
```

## java solution
```java
//用rob(k)代表截止到第k个位置最大的抢劫金额
//rob(k) = max( rob(k-2) + nums[k], rob(k-1) )
class Solution {
    public int rob(int[] nums) {
        if(nums.length==1)return nums[0];
        return Math.max(helper(nums,1,nums.length-1),helper(nums,0,nums.length-2));
    }
    private int helper(int[] nums,int lo,int hi)
    {
        int pre_i1=0,pre_i2=0;
        for(int i=lo;i<=hi;i++)
        {
            int cur=Math.max(nums[i]+pre_i2,pre_i1);
            int temp=pre_i1;
            pre_i1=cur;
            pre_i2=temp;
        }
        return pre_i1;
    }
}
```
