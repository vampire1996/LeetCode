# 54. Spiral Matrix
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/54.%20Spiral%20Matrix/problem.png"/>

## python solution
```python
class Solution:
    def spiralOrder(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: List[int]
        """
        column=len(matrix)
        if column==0:
          return matrix
        row=len(matrix[0])
        direction=1# 1--right 2--left 3--down 4--up
        res=[0 for i in range(column*row)]
        flag=[[1 for i in range(row)]for i in range(column)]
        temp=0
        i,j=0,0
        while temp<column*row:     
            if direction==1:
              while j<row and flag[i][j]!=0:
                res[temp]=matrix[i][j]
                flag[i][j]=0
                j+=1
                temp+=1
              j-=1
              i+=1
              direction=3
            elif direction==2:
              while j>=0 and flag[i][j]!=0:
                res[temp]=matrix[i][j]
                flag[i][j]=0
                j-=1
                temp+=1
              j+=1
              i-=1    
              direction=4
            elif direction==3:
              while i<column and flag[i][j]!=0:
                res[temp]=matrix[i][j]
                flag[i][j]=0
                i+=1
                temp+=1
              j-=1
              i-=1    
              direction=2
            elif direction==4:
              while i>=0 and flag[i][j]!=0:
                res[temp]=matrix[i][j]
                flag[i][j]=0
                i-=1
                temp+=1
              j+=1
              i+=1    
              direction=1
        return res 
```
