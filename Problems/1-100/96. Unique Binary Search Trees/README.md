# 96. Unique Binary Search Trees
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/96.%20Unique%20Binary%20Search%20Trees/problem.png"/>

## python solution
```python
class Solution(object):
    def numTrees(self, n):
        """
        :type n: int
        :rtype: int
        """
        #1256ms 用递归很慢 应该直接用迭代
        if n==1:
            return 1
        if n==2:
            return 2
        if n==3:
            return 5
        num=0
        num+=self.numTrees(n-1)*2
        for i in range(2,n):
            num+=self.numTrees(i-1)*self.numTrees(n-i)
        return num
```

## python3 solution
```python3
class Solution:
    def numTrees(self, n):
        """
        :type n: int
        :rtype: int
        """
        """
        G(n)代表对于的平衡二叉树的数目
        G(n) = G(0) * G(n-1) + G(1) * G(n-2) + … + G(n-1) * G(0) 
        """
        if n==1:
            return 1
        num=[0 for i in range(n+1)]
        num[0],num[1]=1,1
        for i in range(2,n+1):
            for j in range(1,i+1):
                num[i]+=num[j-1]*num[i-j]
        return num[n]  
```
