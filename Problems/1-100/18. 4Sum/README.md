# 18. 4Sum
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/18.%204Sum/problem.png"/>


## python solution
```python
"""
时间复杂度o(n^3)
"""
class Solution(object):
    def fourSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        """
        利用2sum 减少递归次数
        """
        res=[]
        if not nums:
            return res
       
        def findSum(nums,target,N,result,results):
            if len(nums)<N or N<2 or target<nums[0]*N or target>nums[-1]*N:
                return
            if N==2:
                l,r=0,len(nums)-1
                while l<r:
                    s=nums[l]+nums[r]
                    if s==target:
                        results.append(result+[nums[l]]+[nums[r]])
                        l+=1
                        while l<r and nums[l-1]==nums[l]:
                                l+=1
                    elif s<target:
                        l+=1
                    else:
                        r-=1
            else: 
                    a=len(nums)-N+1
                    for i in range(a):
                        if i==0 or(i>0 and nums[i-1]!=nums[i]):
                            findSum(nums[i+1:],target-nums[i],N-1,result+[nums[i]],results)
        findSum(sorted(nums), target, 4, [], res)
        return res  
```

## python3 solution
```python3
class Solution:
    def fourSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        """
        超时了
        """
        """
        is 用于判断两个变量引用对象是否为同一个， == 用于判断引用变量的值是否相等。类似于Java中的equal()和==。反之，is not用于判断两个变量是否引用自不同的对象，而 != 用于判断引用变量的值是否不等。
        只要各对象的值一样，则 x == y 的值一定为True；
         如果对象的类型为整数或字符串且值一样，则 x == y和 x is y 的值为True。（经测试浮点型数值，只有正浮点数符合这条规律 负浮点数不符合）；
        list，tuple，dict，set值一样的话，x is y 则为False；
        x == y 与 x != y 的值相反，x is y 与 x is not y 的值相反。 
        """
        res=[]
        if len(nums)<4:
            return res
        #可推广到N-sum
        def iterator(num,targ,path,cnt,N):
            l=len(num) 
            if cnt==N:
                if targ==0:
                    res.append(path)
                    return 
                else:
                    return
            if not num or l+cnt<N:
                return    
            if l==1:
                if num[0] != targ or cnt != N-1:
                    return    
            for i in range(l):
                 if num[0]*(N-cnt)>targ or num[-1]*(N-cnt)<targ:#最小值乘N-cnt>target 或 最小值乘N-cnt<target
                    return
                 if i==0 or(i>0 and num[i-1]!=num[i]):#消除重复的情况
                        if i<l-1:
                            iterator(num[i+1:],targ-num[i],path+[num[i]],cnt+1,N)     
                        else:    
                            iterator([],targ-num[i],path+[num[i]],cnt+1,N)
        nums.sort()
        iterator(nums,target,[],0,4)
        return res
```
