# 79. Word Search
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/79.%20Word%20Search/problem.png"/>

## python solution
```python
class Solution(object):
    def exist(self, board, word):
        """
        :type board: List[List[str]]
        :type word: str
        :rtype: bool
        """
        """
        思路整理:
        1)遍历整个board 如果满足board[i][j]==word[0]则调用helper 从i,j出发 探索所有可能的路径
        2)利用字典存储满足board[i][j]==word[k]的 i,j位置 每次检测是否在字典中已经出现该位置
        由于一条路径中不能有同一个位置，因此利用dict.has_key(key_value)检测是否存在相同位置
        3)在每个位置 需满足3个条件才能继续递归
        i.有向某一方向前进的余地 
        ii.向该方向前进的元素与word中下一元素相同
        iii.在字典中不存在即将要前进的位置
        4)当获得路径与word相同k==len(word)-1 则成功 返回True
        Explanation
        1)traverse the whole board,if board[i][j]==word[0],call the helper
        2)because he same letter cell may not be used more than once,
        so we use a dictionary to avoid it
        3)in each position,constrains below must be satisfied to continue the recursion
        i.we can move to one direction without oversteping the boundary
        ii.the element we are moving to is the same with next element in word
        iii.there is no same position in dictionary
        4)when we get the same path with word,we can return True
        """
        """
        dict.update(dict2)把字典dict2的键/值对更新到dict里
        dict.has_key(key)如果键在字典dict里返回true，否则返回false
        Dict.pop(key)#pop()，()里为需要删除的key值
        """
        if len(word)>len(board)*len(board[0]):return False
        def helper(i,j,k,Dict):
                if k==len(word)-1:return True
                m=(i-1)*len(board[0])+j
                if i>0 and not Dict.has_key(m)and board[i-1][j]==word[k+1]:#up
                     n={m:True}
                     Dict.update(n)
                     if  helper(i-1,j,k+1,Dict):return True
                     Dict.pop(m)
                m=(i+1)*len(board[0])+j
                if i<len(board)-1 and not Dict.has_key(m)and board[i+1][j]==word[k+1]:#down
                     n={m:True}
                     Dict.update(n)
                     if  helper(i+1,j,k+1,Dict):return True
                     Dict.pop(m)
                m=i*len(board[0])+j-1
                if j>0 and not Dict.has_key(m)and board[i][j-1]==word[k+1]:#left
                     n={m:True}
                     Dict.update(n)
                     if  helper(i,j-1,k+1,Dict):return True
                     Dict.pop(m)
                m=i*len(board[0])+j+1
                if j<len(board[0])-1 and not Dict.has_key(m)and board[i][j+1]==word[k+1]:#right
                     n={m:True}
                     Dict.update(n)
                     if  helper(i,j+1,k+1,Dict):return True
                     Dict.pop(m)
                return False         
        Dict={}
        for i in range(len(board)):
            for j in range(len(board[0])):
                if board[i][j]==word[0]:
                     n={i*len(board[0])+j:True}
                     Dict.update(n)
                     if helper(i,j,0,Dict):return True
                     Dict.pop(i*len(board[0])+j)
        return False
```

## java solution
```java
class Solution {
    public boolean exist(char[][] board, String word) {
        //String为不可变类型 需要将其转换为char数组
        //length--数组长度  length()--字符串长度
        char[ ] w = word.toCharArray();
        for(int i=0;i<board.length;i++)
        {
            for(int j=0;j<board[0].length;j++)
                if(isExist(i,j,0,board,w)) return true;
        }
        return false;
    }
    private boolean isExist(int i,int j,int k,char[][] board,char[] word)
    {
        if (k==word.length)return true;
        if(i<0||j<0||i==board.length||j==board[0].length)return false;
        if(board[i][j]!=word[k])return false;
        //利用异或操作 将当前字符反转 避免出现使用同一个位置字符的情况
        //char 8bit
        board[i][j]^=256;
        boolean result=isExist(i-1,j,k+1,board,word)||
               isExist(i+1,j,k+1,board,word)||
               isExist(i,j-1,k+1,board,word)||
               isExist(i,j+1,k+1,board,word);
        //再次异或 恢复原来的值
        board[i][j]^=256;
        return result;
    }
}
```
