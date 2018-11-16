# 59. Spiral Matrix II
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/59.%20Spiral%20Matrix%20II/problem.png"/>

## python solution
```python
class Solution:
    def generateMatrix(self, n):
        """
        :type n: int
        :rtype: List[List[int]]
        """
        direction=1 #1--right 2--left 3--down 4--up
        res=[[0 for i in range(n)]for i in range(n)]
        i,j=0,0
        temp=1
        while temp<n*n+1:
           if direction==1:
              
              while j<n and res[i][j]==0:
                    res[i][j]=temp
                    temp+=1
                    j+=1
              direction=3
              i=i+1
              j-=1       
           elif direction==2:
              while j>=0 and res[i][j]==0:
                    res[i][j]=temp
                    temp+=1
                    j-=1
              direction=4
              i=i-1
              j+=1
           elif direction==3:
              while i<n and res[i][j]==0:
                    res[i][j]=temp 
                    temp+=1
                    i+=1
              direction=2
              j=j-1
              i-=1
           elif direction==4:
              while i>=0 and res[i][j]==0:
                    res[i][j]=temp
                    temp+=1
                    i-=1
              direction=1
              j=j+1   
              i+=1   
        return res  
```
