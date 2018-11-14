# 46. Permutations
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## python solution
```python
#注意A[:i]代表A[0,i) 左闭右开
class Solution:
    def permute(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        """
        
        
        res=[]
        def permutation(A,path,res): 
          if not A:#判断A是否为空
                res.append(path)
          for i in range(len(A)):
                permutation(A[:i]+A[i+1:], path+[A[i]], res)
        permutation(nums,[],res)
        
        return res
        """
        return [[n] + p
        for i, n in enumerate(nums)# enumerate--枚举nums中元素 i--index n--对应的值
        for p in self.permute(nums[:i] + nums[i+1:])] or [[]]
```
