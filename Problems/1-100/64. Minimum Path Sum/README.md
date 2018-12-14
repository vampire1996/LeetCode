# 64. Minimum Path Sum
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/27.RemoveElement/problem.png "/>


## python solution
```python
class Solution(object):
    def minPathSum(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        """
        思路整理
        res用于存储grid中每一行每个位置到达该位置的最小sum值
        Input:            res
        [
        [1,3,1],          [1,4,5]
        [1,5,1],          [2,7,6]
        [4,2,1]           [6,8,7]
        ]
        1)对于第一行或第一列 res的值可由grid[0][i]+res[i-1](右侧值+当前grid值)
        或 grid[j][0]+res[0](上方值+当前grid值)求得
        2)对于其它情况 res值 为res[i]+grid[j][i](上方值+当前grid值)
        和res[i-1]+grid[j][i](右侧值+当前grid值) 二者之间的最小值
        Explanation
        we use res to store the minimum sum of each position in grid 
        1)for grid[0][i] or grid[j][0],we can simply use grid[0][i]+res[i-1] 
        and grid[j][0]+res[0] to calculate them
        2) for other situation,res[i]=min(res[i]+grid[j][i],res[i-1]+grid[j][i])
        the sum of one particular position,there are only tow potential previous position
        (either from its top or its left side),so we just take the small one
        """
        if not grid:return 0   
        row=len(grid)  
        col=len(grid[0])
        res=[0 for i in range(col)]
        res[0]=grid[0][0]
        for i in range(1,col):res[i]=grid[0][i]+res[i-1]
        for j in range(1,row):
              
            res[0]=grid[j][0]+res[0]
            for i in range(1,col):
                res[i]=res[i]+grid[j][i] if res[i]<res[i-1] else res[i-1]+grid[j][i] 
        
        return res[col-1]
```

## java solution
```java
class Solution {
    public int minPathSum(int[][] grid) {
        int row=grid.length;
        int col=grid[0].length;
        for(int i=0;i<row;i++)
        {
            for(int j=0;j<col;j++)
            {
                if(i==0&&j==0)continue;
                else if(i==0&&j>0) grid[0][j]+=grid[0][j-1];
                else if(i>0&&j==0) grid[i][0]+=grid[i-1][0];
                else grid[i][j]=Math.min(grid[i-1][j]+grid[i][j],grid[i][j]+grid[i][j-1]);
            }
        }
        return grid[row-1][col-1];
    }
}
```
