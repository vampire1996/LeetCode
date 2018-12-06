# 77. Combinations
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/77.%20Combinations/problem.png"/>

## python solution
```python
class Solution(object):
    def combine(self, n, k):
        """
        :type n: int
        :type k: int
        :rtype: List[List[int]]
        """
        """
        recursive version
        思路整理:
        Input: n = 4, k = 2
        1)对于第一个元素,可选得有1，2，3  t=2 有一个元素取不到(4) t=1
        2)对于第二个元素,可选得有2，3，4
        3)因此对于第m个元素。可选的有[m,n-t+1] t为k个元素中剩余所需的元素
        有t-1个元素是取不到的 所以可取上限为n-(t-1)=n-t+1
        Explanation
        1)for the first element,we can choose 1，2，3
        one number we cannot reach(4),so t=1
        2)for the second element,we can choose 2，3，4
        3)thus for the mth element,we can choose element within  [m,n-t+1]
        t is the number of elements we need to add to the current path
        there are t-1 elements we cant reachs,so the upper bound for element
        we can choose is n-(t-1)=n-t+1
        """
        # backtrack--回溯算法
        if k>=n:return [[i for i in range(1,n+1)]]
        def helper(res,lo,hi,path,t):
            if t==0:
                res.append(path)
                return 
            for i in range(lo,hi-t+2):
                helper(res,i+1,hi,path+[i],t-1)
        res=[]
        helper(res,1,n,[],k)
        return res 
```

## python3 solution
```python3
from functools import reduce
class Solution:
    def combine(self, n, k):
        """
        :type n: int
        :type k: int
        :rtype: List[List[int]]
        """
        
        """
        reduce() 函数会对参数序列中元素进行累积。
        函数将一个数据集合（链表，元组等）中的所有数据进行下列操作：
        用传给 reduce 中的函数 function（有两个参数）先对集合中的第 1、2 个元素进行操作，
        得到的结果再与第三个数据用 function 函数运算，最后得到一个结果。
        e.g.reduce(lambda x, y: x+y, [1,2,3,4,5])  # 使用 lambda 匿名函数
        返回15
        """
        """
        思路:
        Input: n = 4, k = 2
        首先将C置为[[1],[2],[3],[4]]
        在遍历C 将小于c[0]的元素插入c最前面 如[4]  插入后为:[1,4] [2,4] [3,4]
        """
        if k>=n:return [[i for i in range(1,n+1)]]
        return reduce(lambda C,_:[[i]+c for c in C for i in range(1,c[0] if c else n+1)],range(k),[[]])
        """
        C,_匿名函数的两个参数
        [[i]+c for c in C for i in range(1,c[0] if c else n+1)]--function
        range(k)迭代次数
        [[]]迭代体
        """
```

## java solution
```java
class Solution {
    public List<List<Integer>> combine(int n, int k) {
        /*
        Input n=7 k=5
        思路整理:
        1)先将k个元素全部置为 如12345
        从最后后一个元素开始逐次加1 12345  12346 12347 12348此时comb[j]=8>n
        则后退1位 并将其+1 12348--12355--12356继续从最后一个元素开始质疑增加
        */
        List<List<Integer>> combs=new ArrayList<>();
        if (n < k) return combs;
        Integer[] comb = new Integer[k];
        for(int i=0;i<k;i++)comb[i]=0;
        int j=0;
        while (j>=0)
        {
            comb[j]++;
            if(comb[j]>n)j--;
            else if(j==k-1)combs.add(new ArrayList<>(Arrays.asList(comb)));
            else
            {
                j++;
                comb[j]=comb[j-1];
            }
        }
        return combs;
            
    }
}
```
