# 29. Divide Two Integers

<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/29.%20Divide%20Two%20Integers/problem.png"/>



## python solution

```python

class Solution(object):
    def divide(self, dividend, divisor):
        """
        :type dividend: int
        :type divisor: int
        :rtype: int
        """
        """
        思路整理：
        1)将b左移bits位直到a-b<0
        循环
        2)若a-b>0则a=a-b从a中减去b cnt加上1<<bits 代表减去了2^bits个abs(divisor)
        3)bits-- b>>=1
        直到bits<0或a减到为零
        """
        if dividend==-2147483648 and divisor==-1: return 2147483647
        sign=-1 if (dividend<0)^(divisor<0) else 1
        a,b=abs(dividend),abs(divisor)
        cnt,bits=0,0
        while a-b>=0:
            b<<=1
            bits+=1
        b>>=1#多移了一位
        bits-=1
        while bits>=0:
            if a-b>0:
                a=a-b
                cnt+=1<<bits  
            elif a-b==0:
                cnt+=1<<bits
                break
            bits-=1
            b>>=1
        return cnt if sign>0 else -cnt
```



## python3 solution

```python3

class Solution:
    def divide(self, dividend, divisor):
        """
        :type dividend: int
        :type divisor: int
        :rtype: int
        """
        if dividend==0: return 0
        if (dividend>0 and divisor>0) or (dividend<0 and divisor<0):
            flag=1
        else:flag=-1
        a,b=abs(dividend),abs(divisor)
        cnt=0
        bits=0
        while a-b>=0:
            b<<=1
            bits+=1
        b>>=1
        bits-=1
        while bits>=0:
            if a-b>0:
                a=a-b
                cnt+=pow(2,bits)
                bits-=1
                b>>=1
            elif a-b==0:
                cnt+=pow(2,bits)
                break
            else:
                bits-=1
                b>>=1
        if cnt>2147483647 : return 2147483647 if flag>0 else -2147483648
        return cnt*flag
```
