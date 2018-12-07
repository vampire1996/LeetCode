# 89. Gray Code
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/112.%20Path%20Sum/problem.png"/>

## python solution
```python
class Solution(object):
    def grayCode(self, n):
        """
        :type n: int
        :rtype: List[int]
        """
        """
        思路整理:
        1)Input: 3
        输出
        0+00 - 0     1+00 - 4
        0+01 - 1  +  1+01 - 5  =[0+grayCode(2),1+grayCode(2)]
        0+11 - 3     1+11 - 6
        0+10 - 2     1+10 - 7
        将第二部分grayCode(2)翻转，得到最终结果
        0+00 - 0     1+10 - 6
        0+01 - 1  +  1+11 - 7  =[0+grayCode(2),1+reverse(grayCode(2))]
        0+11 - 3     1+01 - 5
        0+10 - 2     1+00 - 4
        Output:[0,1,3,2,6,7,5,4] 
        """
        if n==0:return [0] 
        res1=[i for i in self.grayCode(n-1)]
        res2=[pow(2,n-1)+i for i in res1]
        return res1+list(reversed(res2))
```

## python3 solution
```python3
class Solution:
    def grayCode(self, n):
        """
        :type n: int
        :rtype: List[int]
        """
        """
        思路整理
        1)res的长度应为:2^n=1<<n
        2)res中每一位的公式为G(i) = i^ (i/2)
        证明:若G(i)和G(i+1)只有1位不同则得证
        则应证明G(i)^G(i+1) 是2的x次方，即
        i^(i/2) ^ (i+1)^[(i+1)/2]=000000100000 
        i^(i+1) ^ (i/2)^((i+1)/2)=000000100000  
        for x and x+1:
        the result of x^(x+1) is just depended on the low bits.
        There are two cases:
        1.the lowest bit of x is 0, like
        ?????0(? means 0 or 1)
        the x+1 is
        ?????1
        so the x^(x+1) is
        000001
        in this case:(x/2)^((x+1)/2)=
        000000
        the result is
        000001 (2^0)
        2.the lowest bits is 1, like
        ????01111
        the x+1 is
        ????10000
        so the x^(x+1) is
        000011111
        in this case:(x/2)^((x+1)/2)=
        000001111
        the result is
        000010000 (2^5)
        """
        res=[]
        for i in range (1<<n):
            res.append(i^i>>1)
        return res
```

## java solution
```java
/*
My idea is to generate the sequence iteratively. 
For example, when n=3, we can get the result based on n=2.
00,01,11,10 -> (000,001,011,010 ) (110,111,101,100). 
The middle two numbers only differ at their highest bit, 
while the rest numbers of part two are exactly symmetric of part one. 
It is easy to see its correctness.
前一部分只需保持不变，后一部分由res.add(res.get(k)|1<<i)
比如首先k=3 res.get(3)=0b10=3 则res.get(k)|1<<i=110即可加到队尾
*/
class Solution {
    public List<Integer> grayCode(int n) {
       List<Integer> res=new ArrayList();
        res.add(0);
        for(int i=0;i<n;i++)
        {
            int Size=res.size();
            for(int k=Size-1;k>=0;k--) 
                res.add(res.get(k)|1<<i);
        }
        return res;
    }
}
```
