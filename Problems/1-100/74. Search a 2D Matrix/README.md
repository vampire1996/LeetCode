# 74. Search a 2D Matrix
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/74.%20Search%20a%202D%20Matrix/problem.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/74.%20Search%20a%202D%20Matrix/example.png"/>

## python solution
```python
class Solution(object):
    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        """
        思路整理
        1) 当target对于matrix中某一行来说 大于等于其最小值 小于等于最大值
        则在这一行进行二分搜索
        2)若能找到对应元素返回真 否则返回假
        explanation
        1)when row[0]<=target and row[-1]>=target 
        conduct binary search  
        2) if we can find the target in this row,return true
        else return false
        """
        if not matrix or not matrix[0]:return False
        def binarySearch(res):
            lo,hi=0,len(res)
            while lo<hi:
                mi=int((lo+hi)/2)
                if res[mi]==target:return True
                elif res[mi]>target:hi=mi
                else:lo=mi+1
            return False            
        for row in matrix:
            if row[0]<=target and row[-1]>=target:    
                return binarySearch(row)
        return False
```

## python3 solution
```python3
class Solution:
    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        """
        将二维数组看成一个 m*n的一维数组进行二分搜索
        O(log(m*n))=O(log(m))+O(log(n))
        """
        #//  取整除 - 返回商的整数部分（向下取整）
        if not matrix or not matrix[0]:return False
        row,col=len(matrix),len(matrix[0])
        lo,hi=0,row*col
        while lo<hi:
            mi=(lo+hi)//2
            if matrix[mi//col][mi%col]==target:return True
            elif  matrix[mi//col][mi%col]>target:hi=mi
            else:lo=mi+1
        return False
```


## java solution
```java
class Solution {
    /*
    分别对行和列进行二叉搜索O(log(m))+O(log(n))
    */
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix==null||matrix.length==0)return false;
        if(matrix[0]==null||matrix[0].length==0)return false;
        int lo=0,hi=matrix.length,mi=(lo+hi)/2;
        while(lo<hi)
        {
            mi=(lo+hi)/2;
            if(matrix[mi][0]==target)return true;
            else if(matrix[mi][0]<target)lo=mi+1;
            else hi=mi;
        }
        lo=0;
        hi=matrix[0].length;
        //当matrix[mi][0]<target 则在mi这一行进行搜索
        //当matrix[mi][0]>target 则在mi-1这一行进行搜索
        int temp=matrix[mi][0]>target&&mi>0?mi-1:mi;
        while(lo<hi)
        {
            mi=(lo+hi)/2;
            if(matrix[temp][mi]==target)return true;
            else if(matrix[temp][mi]<target)lo=mi+1;
            else hi=mi; 
        }
        return false;
    }
}
```
