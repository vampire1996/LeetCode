# 357. Count Numbers with Unique Digits
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/301-400/357.%20Count%20Numbers%20with%20Unique%20Digits/problem.png"/>

## python solution
```python
class Solution:
    def countNumbersWithUniqueDigits(self, n):
        """
        :type n: int
        :rtype: int
        """
        """
        思路整理
        1.若输入位数大于1
        1)res第一部分是 从0-9 10个数字中取出n个数字并进行全排列combine(10,n)*factorial(n)
        2)以上全排列只能包括n位中只有1个0的情况
        接下来计算n位中多个0的情况
        i. 0x....  x不能是0 且x之后的数位必须含一个0 因此0可以有(n-2)个位置
        0之后数位必须有一个0 其余从1-9中取n-2个数进行全排列即可
        combine(9,n-1)*factorial(n-2)*(n-2)
        ii. 00.... 因为已经有两个0 所以之后n-2位迭代执行
        最高位必须为1-9 任意一个数
        剩下的i-1位 从0-9 中除了上面取出的那个数中取i-1个数 并全排列
        9*combine(9,i-1)*factorial(i-1)
        2.若输入位数等于1 直接返回10
        Explanation
        if n>1
        1)the first part is taking n numbers in 0-9 and taking purmutaion of them
        combine(10,n)*factorial(n)
        2)the upper situation only considers the condition of one 0
        then we talk about the condition when ther are more than 2 0's
        i. 0x....  x cannot be 0 and there must be a 0 after x,
        so 0 can be placed in n-2 positions,
        then we just taking n-2 numbers in 1-9 and take purmutaion of them
        ii. 00.... because there are already 2 0's,so when just iteratively conduct:
        the highest bit must in 1-9
        the rest i-1 bits can anyone but the num in highest bit in 0-9
        9*combine(9,i-1)*factorial(i-1)
        """
        def factorial(num):
            res=1
            for i in range(1,num+1):
                res*=i
            return res
        def combine(n,m):
            temp=min(m,n-m)
            res=1.0
            for i in range(1,temp+1):
                res*=((n-i+1)/i)
            return int(res)
        res=0,0
        res=combine(10,n)*factorial(n)
        for i in range(1,n):
            if i==n-1:res+=combine(9,i-1)*factorial(i-1)*(i-1)
            else:res+=9*combine(9,i-1)*factorial(i-1)
        return res+1 if n>1 else res
```

## java solution
```java
/*
Following the hint. Let f(n) = count of number with unique digits of length n.

f(1) = 10. (0, 1, 2, 3, ...., 9)

f(2) = 9 * 9. Because for each number i from 1, ..., 9, we can pick j to form a 2-digit 
number ij and there are 9 numbers that are different from i for j to choose from.

f(3) = f(2) * 8 = 9 * 9 * 8. Because for each number with unique digits of length 2, say ij, 
we can pick k to form a 3 digit number ijk and there are 8 numbers that are different 
from i and j for k to choose from.

Similarly f(4) = f(3) * 7 = 9 * 9 * 8 * 7....

return f(1) + f(2) + .. + f(n)
*/
class Solution {
    public int countNumbersWithUniqueDigits(int n) {
        if(n==0)return 1;
        int res=10,availableBits=9,pre=9;
        for(int i=n;i>1;i--,availableBits--)
        {
            res+=availableBits*pre;
            pre*=availableBits;
        }
        return res;
    }
}
```
