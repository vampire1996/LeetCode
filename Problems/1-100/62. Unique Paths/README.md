# 62. Unique Paths
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/62.%20Unique%20Paths/problem.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/62.%20Unique%20Paths/example.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/62.%20Unique%20Paths/递归和迭代.png"/>


## python solution
```python
class Solution(object):
    def uniquePaths(self, m, n):
        """
        :type m: int
        :type n: int
        :rtype: int
        """
        if m>n:
            return self.uniquePaths(n,m)
        res=[1 for i in range(m)]
        for i in range(1,n):
          for i in range(1,m):
            res[i]+=res[i-1]
        return  res[m-1] 
```

## python3 solution
```python3
class Solution:
    def uniquePaths(self, m, n):
        """
        :type m: int
        :type n: int
        :rtype: int
        """
        """
        递归方案 速度更慢--超时
        递归调用慢就是指的函数调用带来的参数压栈和退栈所带来的开销
        """
        if m==1 or n==1:
             return 1
        return self.uniquePaths(m-1, n)+self.uniquePaths(m, n-1)  
```

## c solution
```c
/*
This is a combinatorial problem and can be solved without DP. For mxn grid, robot has to move exactly m-1 steps down and n-1 steps right and these can be done in any order.

For the eg., given in question, 3x7 matrix, robot needs to take 2+6 = 8 steps with 2 down and 6 right in any order. That is nothing but a permutation problem. Denote down as 'D' and right as 'R', following is one of the path :-

D R R R D R R R

We have to tell the total number of permutations of the above given word. So, decrease both m & n by 1 and apply following formula:-

Total permutations = (m+n-2)! / (m-1! * n-1!)
*/
int uniquePaths(int m, int n) {
    if(m==1||n==1)
        return 1;
    m--;
    n--;
    int max=m>n?m:n;
    int sum=m+n;
    long long a=1;//long long (__int64) int--long--会溢出
    for(int i=max+1,j=1;i<=sum;i++,j++)
    {
        a*=i;
        a/=j;
    }
    return (int)a;  
}
```
