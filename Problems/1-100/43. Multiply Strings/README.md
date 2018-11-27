# 43. Multiply Strings
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/12.%20Integer%20to%20Roman/problem.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/12.%20Integer%20to%20Roman/example.png"/>

## python solution
```python
class Solution(object):
    def multiply(self, num1, num2):
        """
        :type num1: str
        :type num2: str
        :rtype: str
        """
        """
        string是一种不可变的数据类型 s[1]="e"是错误的
        正确的做法是s=s[:1]+"e"+s[2:]
        """
        """
        manual--手册 手工  trim--修剪
        This is the standard manual multiplication algorithm. We use two nested for loops, working backward from the end of each input number. We pre-allocate our result and accumulate our partial result in there. One special case to note is when our carry requires us to write to our sum string outside of our for loop.
        At the end, we trim any leading zeros, or return 0 if we computed nothing but zeros.
        """
        if num1[0]=='0' or num2[0]=='0':
            return "0"
        l1=len(num1)
        l2=len(num2)
        s=""
        num="0123456789"
        for i in range(l1+l2):
            s+="0"
        i=l1-1
        while i>=0:
            j=l2-1
            carry=0
            while j>=0:
                temp=ord(s[i+j+1])-ord('0')+(ord(num1[i])-ord('0'))*(ord(num2[j])-ord('0'))+carry
                carry=int(temp/10)
                s=s[:i+j+1]+num[temp%10]+s[i+j+2:]
                j-=1
            s=s[:i+j+1]+num[carry]+s[i+j+2:]
            i=i-1
        i=0
        while s[i]=="0":
            i+=1
        return s[i:]
```
## python3 solution
```python3
class Solution:
    def multiply(self, num1, num2):
        """
        :type num1: str
        :type num2: str
        :rtype: str
        """
        """
        思路整理
        Input: num1 = "123", num2 = "456"
        Output: "56088"=3x456+20x456+100x456
        加法利用twosum 要记得补0
        """
        """
        注意 对于python中的字符串 可直接使用s="a"+s 将'a'加到s之前 而不用''.join(reversed(s))
        """
        #很慢 672ms
        if num1[0]=='0' or num2[0]=='0':
            return "0"
        num="0123456789"
        l1=len(num1)
        l2=len(num2)
        def twosum(s1,s2):
            carry=0
            s=""
            l1=len(s1)
            l2=len(s2)
            i=l1-1
            j=l2-1
            while not(i<0 and j<0):
                if i>=0 and j>=0:
                    temp=ord(s1[i])-ord('0')+ord(s2[j])-ord('0')+carry
                    carry=int(temp/10)
                    s=num[temp%10]+s
                    i-=1
                    j-=1
                elif i>=0 and j<0:
                    temp=ord(s1[i])-ord('0')+carry
                    carry=int(temp/10) 
                    s=num[temp%10]+s
                    i-=1
                elif i<0 and j>=0:
                    temp=ord(s2[j])-ord('0')+carry
                    carry=int(temp/10)
                    s=num[temp%10]+s
                    j-=1
            if carry>0: s=num[carry]+s      
            return s
        i=l1-1
        s="0"
        while i>=0:
            s1=""
            j=l2-1
            carry=0
            while j>=0:
                temp=(ord(num1[i])-ord('0'))*(ord(num2[j])-ord('0'))+carry
                carry=int(temp/10)
                s1=num[temp%10]+s1
                j-=1 
            if carry>0: s1=num[carry]+s1
            for k in range(l1-i-1) :
                s1+='0'   
            s=twosum(s1 ,s) 
            i-=1
        return s 
```
