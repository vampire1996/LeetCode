# 50. Pow(x, n)
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## python solution
```python
class Solution(object):
    def myPow(self, x, n):
        """
        :type x: float
        :type n: int
        :rtype: float
        """
        #O(n)很慢
        if x==0:return 0
        if n==0:return 1
        if x==1:return x 
        if x==-1:return x if n%2 else -x
        if n==2147483647 or n==-2147483648:return 0
        num=1.0
        if n>0:
            for i in range(n):
                num=num*x
        else:
            for i in range(-n):
                num=num/x
        return num
```

## python3 solution
```python3
class Solution:
    def myPow(self, x, n):
        """
        :type x: float
        :type n: int
        :rtype: float
        """
        """
        O(logn)
        思路整理
        利用二分法
        1)pow(x,n)=pow(x*x,n/2) if n%2==0
        2)pow(x,n)=x*pow(x*x,n/2) if n%2==1
        """
        if n==0:return 1
        if n<0:
            n=-n
            x=1/x
        return x*self.myPow(x*x,int(n/2)) if n%2 else self.myPow(x*x,int(n/2))
```

## java solution
```java
class Solution {
    public double myPow(double x, int n) {
        //注意java不能将整型直接转换为布尔型 if(n%2)应写成if(n%2==1)
        /*
        For Java solution, it has to handle the case of overflow of Integer. 
        In this case, the value of n has to be carefully handled when n equals 
        to Integer.MIN_VALUE. 
        Hence, better method is to convert n to data type of long
        当n= 2147483648=INT_MIN -n == 2147483648 > INT_MAX发生溢出
        */
        long n_long=n;
        double num=1;
        if(n_long<0){n_long=-n_long;x=1/x;}
        while(n_long>0)
        {
            if((n_long&1)==1)num*=x;
            x=x*x;
            n_long>>=1;
        }
        return num;
    }
}
```

