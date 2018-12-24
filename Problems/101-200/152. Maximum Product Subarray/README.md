# 152. Maximum Product Subarray
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/152.%20Maximum%20Product%20Subarray/problem.png"/>

## python solution
```python
class Solution(object):
    def maxProduct(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        """
        思路整理
        只有两种可能 大写为整数 小写
        1)负数的个数为奇数nums=[a,B,c,D,e,F,g,H,i]
        对于nums必然可以转换为[A,b]或者[a,B]的形式
        (任意一对负数可以组合成一个正数)
        而forward记录正向乘积 back记录反向乘积 即可记录A,B这些值中的最大值
        2)负数的个数为偶数
        将所有数乘起来即可 
        Explanation
          there are only two possible situations:
          1)the number of negetive numbers are even nums=[a,B,c,D,e,F,g,H,i]
           num can be transfered to [A,b]or[a,B]
           we use back and forward to claculate the back product and 
           forward product.so we can use them to find the maximum in A,B's
          2)he number of negetive numbers are odd nums=[a,B,c,D,e,F,g,H,i]
          just return the product of all nums
        """
        res=-2e31
        forward,back=1,1
        l=len(nums)
        for i in range(l):
            forward*=nums[i]
            back*=nums[l-i-1]
            res=max([res,forward,back])
            if back==0:back=1
            if forward==0:forward=1
        return res
```

## java solution
```java
class Solution {
    public int maxProduct(int[] nums) {
      int res=nums[0];
      /*
      用min max存储当前最大和最小的乘积
      如果nums[i]<0 则nums[i]*max<nums[i]*min因此需要将max和min交换
      如果nums[i]=0 
      max=Math.max(nums[i],nums[i]*max)=0;
      min=Math.min(nums[i],nums[i]*min)=0;
      若nums[i+1]>0 
      max=Math.max(nums[i+1],nums[i+1]*max)=nums[i+1];
      min=Math.min(nums[i+1],nums[i+1]*min)=0;
      若nums[i+1]<0 
      max=Math.max(nums[i+1],nums[i+1]*max)=0;
      min=Math.min(nums[i+1],nums[i+1]*min)=nums[i+1];
      min和max中一定有一个保存nums[i+1]
      在接下来的运算中不会会略掉nums[i+1],巧妙地避开了nums[i]=0的情况
      */  
      int max=res,min=res;
      for(int i=1;i<nums.length;i++)
      {
          if(nums[i]<0)
          {
              int temp=max;
              max=min;
              min=temp;
          }
          max=Math.max(nums[i],nums[i]*max);
          min=Math.min(nums[i],nums[i]*min);
          res=Math.max(res,max);
      }
      return res; 
    }
}
```
