# 36. Valid Sudoku
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/16.%203Sum%20Closest/problem.png"/>

## python solution
```python
class Solution(object):
    def isValidSudoku(self, board):
        """
        :type board: List[List[str]]
        :rtype: bool
        """
        """
        '4' in row 7 is encoded as "(4)7".
        '4' in column 7 is encoded as "7(4)".
        '4' in the top-right block is encoded as "0(4)2".
        如果新构建的元素未在集合中出现 则继续 否则返回False
        """
       
        s=set()
        for i in range(9):
            for j in range(9):
                if board[i][j]!='.':
                     temp='('+board[i][j]+')'
                     row=chr(i+ord('0'))+temp
                     column=temp+chr(j+ord('0'))
                     cube=chr(int(i/3)+ord('0'))+temp+chr(int(j/3)+ord('0'))
                     if not(row in s)and not(column in s)and not(cube in s):
                            s.add(row)
                            s.add(column)
                            s.add(cube)
                     else: 
                        return False
        return True              
```


## python3 solution
```python3
class Solution:
    def isValidSudoku(self, board):
        """
        :type board: List[List[str]]
        :rtype: bool
        """
        for i in range(9):
            cnt=[0 for i in range(9)]
            for j in range(9):
                if board[i][j]!='.':
                    if cnt[ord(board[i][j])-ord('0')-1]!=0:
                        return False
                    else:
                        cnt[ord(board[i][j])-ord('0')-1]+=1
        for i in range(9):
            cnt=[0 for i in range(9)]                 
            for j in range(9):
                if board[j][i]!='.':
                    if cnt[ord(board[j][i])-ord('0')-1]!=0:
                        
                        return False
                    else:
                        cnt[ord(board[j][i])-ord('0')-1]+=1                                  
        m,n=0,0
        while m<9:
          n=0                  
          while n<9:  
             
             cnt=[0 for i in range(9)]                
             for i in range(m,m+3):            
                   for j in range(n,n+3):
                        if board[i][j]!='.':
                            if cnt[ord(board[i][j])-ord('0')-1]!=0:
                                 return False
                            else:
                                 cnt[ord(board[i][j])-ord('0')-1]+=1    
             n+=3
          m+=3
        return True  
```
