# 73. Set Matrix Zeroes
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/73.%20Set%20Matrix%20Zeroes/problem.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/73.%20Set%20Matrix%20Zeroes/example.png"/>


## python solution
```python
class Solution(object):
    def setZeroes(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: void Do not return anything, modify matrix in-place instead.
        """
        """
        My idea is simple: store states of each row in the first of that row, and store states of each column in the first of that column. Because the state of row0 and the state of column0 would occupy the same cell, I let it be the state of row0, and use another variable "col0" for column0. In the first phase, use matrix elements to set states in a top-down way. In the second phase, use states to set matrix elements in a bottom-up way.
        """
        #O(1) space
        if not matrix:
            return matrix
        rows=len(matrix)
        cols=len(matrix[0])
        col0=1
        for i in range(rows):
            if matrix[i][0]==0: col0=0
            for j in range(1,cols):
                if matrix[i][j]==0:
                    matrix[i][0]=matrix[0][j]=0
        #必须使用倒序  
        i=rows-1
        j=cols-1
        while i>=0:
            j=cols-1
            while j>=1:  
                if matrix[i][0]==0 or matrix[0][j]==0:
                    matrix[i][j]=0
                j-=1
            if col0==0: matrix[i][0]=0
            i-=1
```

## python3 solution
```python3
class Solution:
    def setZeroes(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: void Do not return anything, modify matrix in-place instead.
        """
        #O(m+n) space
        if not matrix:
            return matrix
        def find(res,x):
            if not res:
                return False
            for i in res:
                 if i==x:
                        return True
            return False
        row=[]
        column=[]
        lenRow=len(matrix) 
        lenColumn=len(matrix[0]) 
        for i in range(lenRow):
            for j in range(lenColumn):
                if matrix[i][j]==0:
                    if not find(row,i):
                        row.append(i)
                    if not find(column,j):
                        column.append(j)
        print(row,column)                
        for i in row:
            for j in range(lenColumn):
                 matrix[i][j]=0
        for i in range(lenRow):
            for j in column:
                 matrix[i][j]=0
```
