# 48. Rotate Image
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/48.%20Rotate%20Image/problem.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/48.%20Rotate%20Image/example.png"/>

## python solution
```python
class Solution(object):
    def rotate(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: void Do not return anything, modify matrix in-place instead.
        """
        """
        b = a[i:j:s]表示：i,j与上面的一样，但s表示步进，缺省为1.
        所以a[i:j:1]相当于a[i:j]
        当s<0时，i缺省时，默认为-1. j缺省时，默认为-len(a)-1
        所以a[::-1]相当于 a[-1:-len(a)-1:-1]，也就是从最后一个元素到第一个素复制一遍，即倒序。
        
        zip() 函数用于将可迭代的对象作为参数，将对象中对应的元素打包成一个个元组，然后返回由这些元组组成的列表。
        
        多个实参，放到一个元组里面,以*开头，可以传多个参数；**是形参中按照关键字传值把多余的传值以字典的方式呈现
        """
        
        """
        * clockwise rotate
        * first reverse up to down, then swap the symmetry 
        * 1 2 3     7 8 9     7 4 1
        * 4 5 6  => 4 5 6  => 8 5 2
        * 7 8 9     1 2 3     9 6 3
                [::-1]     zip
        """
        matrix[:] = zip(*matrix[::-1])
```

## python3 solution
```python3
class Solution:
    def rotate(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: void Do not return anything, modify matrix in-place instead.
        """
        res=[]
        row=len(matrix)
        column=len(matrix[0])
        i=row-1
        j=0
        while i>=0:
          j=0  
          for j in range(column):   
            res.append(matrix[i][j])
          i-=1
        i=0
        j=0
        k=0
        for j in range(column):
            i=0
            for i in range(column):
                matrix[i][j]=res[k]
                k+=1
```
