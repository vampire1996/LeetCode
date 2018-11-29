# 5. Longest Palindromic Substring
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/5.%20Longest%20Palindromic%20Substring/problem.png"/>

## python solution
```python
class Solution(object):
    def myAtoi(self, str):
        """
        :type str: str
        :rtype: int
        """
        if not str:return 0
        l=len(str)
        integer=0
        i=0
        flag=1
        while i<l and str[i]==' ':i+=1
        if i==l:return 0 
        if  str[i]=='+' or str[i]=='-':
            flag=1-(str[i]=='-')*2
            i=i+1
        if i==l:return 0 
        while i<l and ord(str[i])>=ord('0') and ord(str[i])<=ord('9'):
            integer=integer*10+ord(str[i])-ord('0')
            i+=1
        if integer>2147483647:
                if flag==1:return 2147483647
                else:return -2147483648
        return integer*flag    
```

## python3 solution
```python3
class Solution:
    def myAtoi(self, str):
        """
        :type str: str
        :rtype: int
        """
        if not str:return 0
        l=len(str)
        integer=0
        i=0
        flag=1
        #首先去掉队首的空格
        while i<l and str[i]==' ':
            i+=1
        if i>=l:return 0 
        #若第一个非空格字符不是数字也不是正负号 则返回0
        if not(ord(str[i])>=ord('0')and ord(str[i])<=ord('9'))and str[i]is not'+'and str[i]is not'-':
            return 0
        #若第一个非空格字符是正负号 则i+1 置符号位
        if str[i]=='+' or str[i]=='-':
            if str[i]=='+':
                i=i+1
            else:
                i=i+1
                flag=-1
        if i>=l:return 0
        #若正负号后第一个字符不是数字则返回0
        if not(ord(str[i])>=ord('0')and ord(str[i])<=ord('9')): return 0
        #去掉数字队列开头的0
        while i<l and str[i]=='0':
            i+=1   
        if i>=l:return 0 
        while i<l and ord(str[i])>=ord('0')and ord(str[i])<=ord('9'):
            integer+=ord(str[i])-ord('0')
            integer*=10
            i+=1
        #多乘了一个10 因此要除回来
        integer=flag*int(integer/10)
        if integer>= 2147483647:
            return 2147483647
        if integer<=-2147483648:
            return -2147483648
        return  integer
             
```
