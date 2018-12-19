# 120. Triangle
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## python solution
```python
class Solution(object):
    def minimumTotal(self, triangle):
        """
        :type triangle: List[List[int]]
        :rtype: int
        """
        """
        思路整理
        用cur和pre记录当前行和之前一行到达每个位置的最小路径和
        pre                 a b c
        triangle[i]        d e f g    cur a+d min(a,b)+e min(b,c)+e c+g
        按以上计算方法即可
        Explanation
        we use cur and pre to store the minimun sum to one position 
        in the current row and the previous row
        """
        #O(row^2) time complexity  O(row) space complexity
        minSum=2147483647#MAX_INT
        cur=[triangle[0][0]]
        for i in range(1,len(triangle)):
            pre=[m for m in cur]
            for j in range(len(triangle[i])): 
                if j!=len(triangle[i])-1 and j!=0:
                    cur[j]=min(pre[j],pre[j-1])+triangle[i][j]
                elif j==0:cur[j]=pre[0]+triangle[i][0]
                else:cur.append(pre[j-1]+triangle[i][j])
        for num in cur:
            if minSum>num:minSum=num 
        return minSum
```
