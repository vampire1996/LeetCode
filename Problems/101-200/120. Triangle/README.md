# 120. Triangle
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/120.%20Triangle/problem.png"/>

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


## java solution
```java
/*
采用自底而上(bottom up)的动态规划算法
如果已知triangle中  某一位置及其左右两个"孩子" a  则经过a到底的路径一定是a+min(b,c)
                                           b c
根据这种思路 我们从triangle的最后一行开始 每个位置记录从该位置出发到底的最小路径和 
则有 triangle[i][j]=min(triangle[i+1][j],triangle[i+1][j+1])+triangle[i][j] 
则triangle[0][0] 最终存储的就是最小路径和
*/
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        for(int i=triangle.size()-2;i>=0;i--)
        {
            for(int j=0;j<triangle.get(i).size();j++)
            {
                int self=triangle.get(i).get(j);
                int min=Math.min(triangle.get(i+1).get(j),triangle.get(i+1).get(j+1));
                triangle.get(i).set(j,self+min);
            }
        }
        return triangle.get(0).get(0);
    }
}
···
