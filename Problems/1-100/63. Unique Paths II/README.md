# 63. Unique Paths II
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/63.%20Unique%20Paths%20II/problem.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/63.%20Unique%20Paths%20II/example.png"/>

## python solution
```python
class Solution(object):
    def uniquePathsWithObstacles(self, obstacleGrid):
        """
        :type obstacleGrid: List[List[int]]
        :rtype: int
        """
        """
        思路整理:
        1)对于任何一个位置，在该位置只能向下或者向左运动，因此在该位置到达终点的路径数为
        temp[n(cur)]=temp[n(pre)]+temp[n-1(cur)] 
        tem[n(cur)]--当前位置 tem[n-1(cur)]--当前右侧 temp[n(pre)]--当前下方
        2)对于有路障的情况,在终点所在那一行的最左侧路障左侧temp均为0--无法到达终点 右侧均为1--可到达终点
        Input:00000x00x00  temp--00000000011 注意temp[0]在最左侧
        3)对于终点以上的位置来说
        i:temp[n(cur)]=temp[n(pre)]+temp[n-1(cur)] --当该位置无路障
        ii:temp[i]=0--当该位置有路障
        4)注意要检查终点所在列 temp[0]=0--当该位置有路障
        e.g.
        Input:            temp:
        
         0,0,0,0,0,0,0,1       3,3,3,3,3,2,1,0 
         0,1,0,1,0,0,0,0       0,0,0,0,1,1,1,1
         0,0,0,0,0,1,1,0       0,0,0,0,0,0,0,1
        How to solve it:
        1)For any position,the robot can only move either up or right,so the number of the paths the robot 
        can move to the destination is the sum of temp[n(pre)] and temp[n-1(cur)] 
        2)AS far as the obstacle situation,when robot is in the same row with the destination
        in the left side of the obstacle with largest index in the last row of Grid
        elements of temp are all 0,while in the right side,they are all 1,
        which means that in these positions the robot can get to the destination
        3)when robot is not in the same row with the destination
        when there is no obstacle in one point,temp[n(cur)]=temp[n(pre)]+temp[n-1(cur)]
        when there is one obstacle in one point,temp[i]=0
        4)To be noticed,we should check the same column with the finish point,
        if there are obstacles,set temp[0] to zreo
        """
        row=len(obstacleGrid)
        col=len(obstacleGrid[0])
        if obstacleGrid[row-1][col-1]==1 or obstacleGrid[0][0]==1:return 0
        temp=[1 for i in range(col)]
        for i in range(col):
            if obstacleGrid[row-1][col-1-i]==1:
                temp[i:]=[0 for j in range(col-i)]
                break
        for j in range(1,row):
            for i in range(1,col):
                if obstacleGrid[row-j-1][col-1]==1:temp[0]=0
                if obstacleGrid[row-j-1][col-1-i]==1:temp[i]=0
                else:temp[i]+=temp[i-1] 
        return temp[col-1]        
```

## python3 solution
```python3
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid):
        """
        :type obstacleGrid: List[List[int]]
        :rtype: int
        """
        """
       obstacleGrid =  0,0,0
                       0,1,0
                       0,0,0
          index of dp 0,1,2,3
         first time   0,1,1,1
         sec   time   0,1,0,1
         third time   0,1,1,2
      
     
       obstacleGrid =  0,0,0
                       0,0,0
                       0,0,0
          index of dp 0,1,2,3
         first time   0,1,1,1
         sec   time   0,1,2,3
         third time   0,1,3,6
        """
        row=len(obstacleGrid)
        col=len(obstacleGrid[0])
        dp=[0 for i in range(col)]
        dp[0]=1
        for i in range(row):
            for j in range(col):
                if obstacleGrid[row-i-1][col-j-1]==1:
                    dp[j]=0
                elif j>0 and obstacleGrid[row-i-1][col-j-1]==0:
                    dp[j]+=dp[j-1]
        return dp[col-1]
```
