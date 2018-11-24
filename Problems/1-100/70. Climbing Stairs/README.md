# 70. Climbing Stairs
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/70.%20Climbing%20Stairs/problem.png"/>

## c solution
```c
int climbStairs(int n) {
    int a=1,b=1,temp;
    for(int i=0;i<n;i++)
    {
        temp=a;
        a=b;
        b=temp+b;
    }
    return a;
}
```

## python solution
```python
class Solution:
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        a,b=1,1
        #斐波那契数列 n 的总步数是sum(n-1+1step,n-2+2step ) 
        for _ in range(n):
            a,b=b,a+b
        return  a
```
