# 130. Surrounded Regions
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/130.%20Surrounded%20Regions/problem.png"/>

## python solution
```python
class Solution(object):
    def solve(self, board):
        """
        :type board: List[List[str]]
        :rtype: void Do not return anything, modify board in-place instead.
        """
        """
        DFS
        思路整理:
        1)找到所有未被包围的'O' 而这种'O'只能是从board的第一行，第一列，最后一行，最后一列
        出发的一系列'O'
        2)从上述位置出发进行DFS 也就是向上 向下 向左 向右移动 
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
class Solution {
    int[][] dirs={{0,1},{0,-1},{1,0},{-1,0}};
    public void solve(char[][] board) {
        if(board==null||board.length==0||board[0]==null||board[0].length==0)
            return;
        int row=board.length,col=board[0].length;
        for(int i=0;i<row;i++)
        {
            if(board[i][0]=='O')
            {
                dfs(board,i,0);
            }
            if(board[i][col-1]=='O')
            {
                dfs(board,i,col-1);
            }
        }
        for(int j=0;j<col;j++)
        {
            if(board[0][j]=='O')
            {
                dfs(board,0,j);
            }
            if(board[row-1][j]=='O')
            {
                dfs(board,row-1,j);
            }
        }
        for(int i=0;i<row;i++)
        {
            for(int j=0;j<col;j++)
            {
                if(board[i][j]=='O')
                {
                    board[i][j]='X';
                }
                else if(board[i][j]=='*')
                {
                    board[i][j]='O';
                }
            }
        }
    }
    
    private void dfs(char[][] board,int i,int j)
    {
        int m = board.length, n = board[0].length;
        board[i][j] = '*';
        for(int[] dir:dirs)
        {
            int x=i+dir[0];
            int y=j+dir[1];
            if(x<0||x==m||y<0||y==n|| board[x][y] != 'O')continue;
            dfs(board,x,y);
        }
    }     
}
```

## python3 solution
```python3
class Solution:
    def solve(self, board):
        """
        找到所有未被包围的'O' 将其置为'S'
        """
        #board=[[]] return 
        if not any(board):return 
        row,col=len(board),len(board[0])
        save=[ij for k in range(max(row,col)) for ij in ((k,0),(0,k),(row-1,k),(k,col-1))]
        while save:
            i,j=save.pop()
            if 0<=i<row and 0<=j<col and board[i][j]=='O':
                board[i][j]='S'
                save.extend([(i-1,j),(i+1,j),(i,j-1),(i,j+1)])
        #p=='S'=1   'XO'[1]='O' 之前将未被包围的'O'置为'S'，再将其变回来
        #p=='S'=0   'XO'[0]='X' 被包围的'O'置为'X'
        """
        board1[:]=[['XO'[p=='S'] for p in r] for r in board1]
        board2=[['XO'[p=='S'] for p in r] for r in board2]
        board1的操作是更改board1内部的值，board2的操作是重新生成一个对象赋值给board2
        board2指向的地址还是原来的
        """
        board[:]=[['XO'[p=='S'] for p in r] for r in board]
```
