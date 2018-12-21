# 264. Ugly Number II
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/201-300/264.%20Ugly%20Number%20II/problem.png"/>

## python solution
```python
class Solution(object):
    def nthUglyNumber(self, n):
        """
        :type n: int
        :rtype: int
        """
        """
        思路整理
        1)用seq[0:n]存储第1个到第n个ugly number
        2)计算第i个ugly number的方法是min(seq[x]*2,seq[y]*3,seq[z]*5)
        x,y,z是在序列中未出现的分别乘以2，3，5 的最小指针
        也就是说如果seq[i]=seq[x]*2
        x指针对应的元素已经乘过2 并在队列中存储了 下一个大于它且同样乘以2的元素就是seq[x+1]
        We have an array seq of first n ugly number. We only know, at the beginning,
        the first one, which is 1. 
        Then seq[1] = min( seq[0]x2, seq[0]x3, seq[0]x5). The answer is seq[0]x2. 
        So we move 2's pointer to 1. 
        Then we test:
        seq[2] = min( seq[1]x2, seq[0]x3, seq[0]x5). 
        And so on. Be careful about the cases such as 6, 
        in which we need to forward both pointers of 2 and 3.
        """
        seq=[1 for i in range(n)]
        p2,p3,p5=0,0,0
        for i in range(1,n):
            num=min(seq[p2]*2,min(seq[p3]*3,seq[p5]*5))
            seq[i]=num
            #注意以下情况不是 if elseif 的关系 而是并列的关系
            #seq[p2]=3  seq[p3]=2
            #2*3=6 3*2=6 seq[i]=6 所以这两种情况都已经使用过了
            #因此均需要向前移动指针p2++ p3++
            if num==seq[p2]*2:p2+=1
            if num==seq[p3]*3:p3+=1
            if num==seq[p5]*5:p5+=1                
        return seq[n-1]
```

## java solution
```java
class Solution {
    public int nthUglyNumber(int n) {
        int[] seq=new int[n];
        int p2=0,p3=0,p5=0;
        seq[0]=1;
        for(int i=1;i<n;i++)
        {
            int num=Math.min(seq[p2]*2,Math.min(seq[p3]*3,seq[p5]*5));
            seq[i]=num;
            if(num==seq[p2]*2)p2++;
            if(num==seq[p3]*3)p3++;
            if(num==seq[p5]*5)p5++;
        }
        return seq[n-1];
    }
}
```
