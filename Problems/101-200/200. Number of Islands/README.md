# 200. Number of Islands
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/80.%20Remove%20Duplicates%20from%20Sorted%20Array%20II/problem.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/80.%20Remove%20Duplicates%20from%20Sorted%20Array%20II/example.png"/>

## python solution
```python
class Solution(object):
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        """
        思路整理DFS
        1)用visited标记所有访问过的'1'
        2)利用helper找到所有与当前位置相通的'1'，并在visited中将其标记为已访问
        3)在主循环中每次遇到一个未访问过的'1' 执行一次DFS 也就是说找老了一个新的
        island 所以num++
        Explanation
        1)we use 'visited' to store all the positions of visited '1's
        2)function helper can help us to find all the '1's which is connected to 
        current '1',and mark them to Ture in 'visited'
        3)in main iteration,when we meet a '1' which has not been visited,
        we call function helper and also ,this means that we find a new island
        so num++
        """
        if not grid:return 0
        def helper(visited,i,j,row,col):
            if i<0 or i==row or j<0 or j==col:
                return 
            if visited[i][j]==True or grid[i][j]=='0':return 
            visited[i][j]=True
            helper(visited,i+1,j,row,col)
            helper(visited,i-1,j,row,col)
            helper(visited,i,j+1,row,col)
            helper(visited,i,j-1,row,col)
        visited=[[False for i in range(len(grid[0]))]for j in range(len(grid))]
        row,col=len(grid),len(grid[0])
        num=0
        for i in range(row):
            for j in range(col):
                if visited[i][j]==True or grid[i][j]=='0':continue
                helper(visited,i,j,row,col)
                num+=1
        return num
```


## python3 solution
```python3
class Solution:
    def numIslands(self, grid):
        """
        Python 2.7 doc on map --返回一个列表
        "Apply function to every item of iterable and return a list of the results."
        Python 3.6 doc on map --返回一个迭代器
        "Return an iterator that applies function to every item of iterable, yielding the results."
        在python3中,map返回一个迭代器,将结果不断迭代,计算的结果会作与下次结果叠加
        如
        Input:
        11110
        11010
        11000
        00000
        map(sink,(i+1,i-1,i,i),(j,j,j+1,j-1))输出 9(将所有1求和)
        list(map(sink,(i+1,i-1,i,i),(j,j,j+1,j-1))) 输出 1
        """
        def sink(i,j):
            if 0<=i<len(grid) and 0<=j<len(grid[0]) and grid[i][j]=='1':
                grid[i][j]='0'
                list(map(sink,(i+1,i-1,i,i),(j,j,j+1,j-1)))
                return 1
            return 0
        if not grid:return 0
        return sum(sink(i,j) for i in range(len(grid)) for j in range(len(grid[0])))
```

## java solution
```java
class Solution {
    private int row,col;
    public int numIslands(char[][] grid) {
        if(grid==null||grid.length==0)return 0;
        row=grid.length;
        col=grid[0].length;
        int islands=0;
        for(int i=0;i<row;i++)
        {
            for(int j=0;j<col;j++)
                islands+=sink(grid,i,j);
        }
        return islands;
    }
    private int sink(char[][] grid,int i,int j)
    {
        if(i<0||i==row||j<0||j==col||grid[i][j]=='0')return 0;
        grid[i][j]='0';
        for(int k=0;k<4;k++)
        {
            sink(grid,i+d[k],j+d[k+1]);
        }
        return 1;
    }
    int[] d={1,0,-1,0,1};
}
```
