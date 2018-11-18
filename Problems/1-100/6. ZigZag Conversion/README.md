# 6. ZigZag Conversion
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/6.%20ZigZag%20Conversion/problem.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/6.%20ZigZag%20Conversion/example.png"/>

## python solution
```python
"""
60ms
"""
class Solution(object):
    def convert(self, s, numRows):
        """
        :type s: str
        :type numRows: int
        :rtype: str
        """
        l=len(s)
        if numRows==1 or l<=numRows:
            return s
        i=0
        res=["" for j in range(numRows)]  
        index=0
        while i<l:
          index=0
          while index<numRows:
             if i==l:
               break
             res[index]+=s[i]
             index+=1
             i+=1  
          index=numRows-2
          while index>0:
              if i==l:
                break  
              res[index]+=s[i]
              index-=1
              i+=1
        index=1
        while index<numRows:
            res[0]+=res[index]
            index+=1
        return  res[0] 
```
## python3 solution
```python3
"""
我的方案 超时了
"""
class Solution:
    def convert(self, s, numRows):
        """
        :type s: str
        :type numRows: int
        :rtype: str
        """
        l=len(s)
        if l==0:
            return s
        if numRows==1 or numRows >= len(s):
            return s
        res=[]
        ret=""
        i=0
        column=0
        row=0
        temp=0
        while i<l:
          a=[]
          while row<numRows:
            if i==l:
              a.append(0)
            elif column==0:
              a.append(s[i])
              i+=1
            else:
              if row+column==numRows-1:
                  a.append(s[i])
                  i+=1
              else:
                  a.append(0)
            row+=1
          res.append(a)  
          row=0  
          column+=1 
          temp+=1
          if column==numRows-1:
            column=0
        i=0
        j=0
        while i<numRows:
            while j<temp:
                if res[j][i] !=0:
                    ret+=(res[j][i])
                j+=1
            j=0
            i+=1    
        return ret  
```
