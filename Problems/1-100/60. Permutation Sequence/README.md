# 60. Permutation Sequence
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/12.%20Integer%20to%20Roman/problem.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/12.%20Integer%20to%20Roman/example.png"/>

## python solution
```python
class Solution:
    def getPermutation(self, n, k):
        """
        :type n: int
        :type k: int
        :rtype: str
        """
        #可以将阶乘保存成数组这样时间复杂度由O(n^2)->O(n)
        fac=[1 for i in range(n+1)]
        for i in range(2,n+1):
              fac[i]=fac[i-1]*i
        num="123456789"
        s=""
        #subtract 1 because of things always starting at 0
        k=k-1
        while n>0:
             temp=int(k/fac[n-1])
             s+=num[temp]
             num=num[:temp]+num[temp+1:]
             k=k%fac[n-1]
             n=n-1
        return s   
```
## python3 solution
```python3
class Solution:
    def getPermutation(self, n, k):
        """
        :type n: int
        :type k: int
        :rtype: str
        """
        #可以将阶乘保存成数组这样时间复杂度由O(n^2)->O(n)
        def factorial(n):
            num=1
            for i in range(2,n+1):
                num*=i
            return num   
        num="123456789"
        s=""
        #subtract 1 because of things always starting at 0
        k=k-1
        while n>0:
             fac=factorial(n-1)
             temp=int(k/fac)
             s+=num[temp]
             num=num[:temp]+num[temp+1:]
             k=k%fac 
             n=n-1
        return s
```
