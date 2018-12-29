# 279. Perfect Squares
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/201-300/279.%20Perfect%20Squares/problem.png"/>

## python solution
```python
class Solution(object):
    def numSquares(self, n):
        """
        :type n: int
        :rtype: int
        """
        """
        O(n^3)
        思路整理:
        1)用nums存储小于根号n取整的所有整数的平方和
        2)迭代执行O(n)
           以nums[i]为组成n的平方数中的最大值
           j=i
           迭代执行O(j)
              找到以nums[0:j+1]中平方数组成n-nums[i]的最小平方数个数--O(j)
        Explanation
        1)use nums to store all square numbers of integers which are less
        than int(sqrt(n))
        2)iteratively conduct
             take nums[i] as the largest number as a part of n
             iteratively conduct
                find the smallest number of n-nums[i]'s square numbers
                using nums[0:j+1]
        """
        def helper(nums,lo,hi,temp):
            if temp==0:return 0
            i=hi
            cnt=0
            while i>=lo:
                if temp-nums[i]>0:
                    temp-=nums[i]
                    cnt+=1
                    continue
                elif temp-nums[i]==0:break
                else:i-=1
            return cnt+1
        num=int(math.sqrt(n))
        nums=[i*i for i in range(1,num+1)]
        cnt=2e31  
        i=num-1
        while i>=0:
            j=i
            while j>=0:
                cur=helper(nums,0,j,n-nums[i])
                if cur+1<cnt:cnt=cur+1
                j-=1   
            i-=1
        return cnt
```

## python3 solution
```python
class Solution:
    _dp=[0]
    def numSquares(self, n):
        """
        :type n: int
        :rtype: int
        """
        """
        static dynamic programming
        用dp数组存储每一个数到该位置所需的最小平方数个数
        那么dp[j]=min(dp[j-i*i])+1 1<=i*i<=j 
        j=j-i*i+i*i 也就是说每个数都可以由cnt[j-i*i]+1得到一个平方数和的方案
        找到其中最小的个数即可
        这里利用静态变量_dp，只需初始化一次 当之前有testcase调用之后，之前的_dp继续可以用与下一次
        testcase使用,因此可以减少时间
        """
        mincnt=self._dp
        while len(mincnt)<=n:
            mincnt+=[min(mincnt[-i*i] for i in range(1,int(len(mincnt)**0.5)+1))+1]
        return mincnt[n]
```

## java solution
```java
class Solution {
    public int numSquares(int n) {
        return LagrangeFourSquareTheorem(n);
    }
    /*
    广度优先搜索       search       search
    Input: n = 13        1         2(1+1)
                         4         5(1+4)
                         9         10(1+9)
                        cnt=1      13(9+3)  结果为2
                                   cnt=2

    */
    private int bfs(int n)
    {
        if(n<=0)return 0;
        List<Integer> squares=new ArrayList<Integer>();
        boolean visited[]=new boolean[n];
        for(int i=1;i*i<=n;i++)
        {
            if(i*i==n)return 1;
            squares.add(i*i);
        }
        Queue<Integer> search = new LinkedList<Integer>();
        for(int i=1;i*i<=n;i++)search.add(i*i);
        int curCnt=1;
        while(!search.isEmpty())
        {
            curCnt++;
            int searchSize=search.size();
            for(int i=0;i<searchSize;i++)
            {
                int tmp=search.peek();
                //当前search中某一数加上一个平方数如果等于n则搜索结束
                for(int square:squares)
                {
                   if(tmp+square==n)
                       {
                       return curCnt;
                       }
                   //visited 用于存储是否访问过某一节点，如果访问过则不再访问 
                   else if(tmp+square<n&&visited[tmp+square-1]==false)
                   {
                    search.add(tmp+square);
                   visited[tmp+square-1]=true;
                   }
                   else if(tmp+square>n) break;
                }
                search.remove();
            }
        }
        return 0;
    }
    //Lagrange  四平方定理： 任何一个正整数都可以表示成不超过四个整数的平方之和。
    //O(n)
    private int LagrangeFourSquareTheorem(int n) 
    {
        int ub=(int)Math.sqrt(n);//upper bound
        for(int a=0;a<=ub;a++)
        {
            for(int b=a;b<=ub;b++)
            {
                //因为a,b都是从0开始的,所以返回时的数一定是最小的
                int c=(int)Math.sqrt(n-a*a-b*b);
                if(a*a+b*b+c*c==n)
                {
                    return (a==0?0:1)+(b==0?0:1)+(c==0?0:1);
                }
            }
        }
        //超过3个只能是4
        return 4;
    }
}
```
