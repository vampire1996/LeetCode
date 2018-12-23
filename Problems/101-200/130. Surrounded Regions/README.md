# 130. Surrounded Regions
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## python solution
```python
class Solution(object):
    def solve(self, board):
        """
        :type board: List[List[str]]
        :rtype: void Do not return anything, modify board in-place instead.
        """
        """
        BFS
        思路整理:
        1)找到所有未被包围的'O' 而这种'O'只能是从board的第一行，第一列，最后一行，最后一列
        出发的一系列'O'
        2)从上述位置出发进行BFS 也就是向上 向下 向左 向右移动 
        看接下来移动到的位置是否是'O' 若不是，则返回
        3)利用isSurrounded 存储未被包围和被包围的'O'的位置
        将对应位置board中元素置为'X'即可
        Explanation
        1)try to find all 'O's,which can only be a part of a series of 'O's started 
        from the 1st row.1st column,last row,last column
        2)start from one position,try to do BFS,which means that we are trying to 
        move to the left,right,up and down position
        then check the current element,if it's 'O',set isSurrounded[i][j]=False  
        and continue BFS
        else return
        3)we use isSurrounded to store all positions of surrended 'O's and not
        surrended 'O's
        so just set the element to 'X' in corresponding posiotion in board
        """
        def helper(isSurrounded,i,j):
            if i==0 or j==0 or i==len(board)-1 or j==len(board[0])-1:return
            if isSurrounded[i][j]==False or board[i][j]=='X':return
            isSurrounded[i][j]=False  
            helper(isSurrounded,i+1,j)
            helper(isSurrounded,i,j+1)
            helper(isSurrounded,i-1,j)
            helper(isSurrounded,i,j-1)
        if len(board)<=2 or len(board[0])<=2:return
        isSurrounded=[[True for i in range(len(board[0]))]for j in range(len(board))]
        for j in range(1,len(board)-1):
            if board[j][0]=='O':helper(isSurrounded,j,1)
            if board[j][len(board[0])-1]=='O':helper(isSurrounded,j,len(board[0])-2)
        for i in range(1,len(board[0])-1):
            if board[0][i]=='O':helper(isSurrounded,1,i)
            if board[len(board)-1][i]=='O':helper(isSurrounded,len(board)-2,i)
        for j in range(1,len(board)-1):
             for i in range(1,len(board[0])-1):
                    if board[j][i]=='O':
                        if isSurrounded[j][i]==True:board[j][i]='X'
```

## java solution
```java

```
