# 8. String to Integer (atoi)
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/5.%20Longest%20Palindromic%20Substring/problem.png"/>

## python solution
```python
class Solution(object):
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        """
        思路整理
        s[i]从s的第二个元素开始 从右向左扫描
        1)若s[i+1]==s[i-1]  其左右指针依次向右拓展 如:   <----bb---->
        2)若s[i]==s[i-1]  其左右指针依次向右拓展 如:   <----bb---->
        记录最长的right-left
        注意:以上两种情况应分别讨论 而不是对立的 反例:aaaa
        """
        l=len(s)
        i=1
        leftPal=0
        rightPal=0
        while i<l:
            if i<l-1 and s[i+1]==s[i-1]:
                left=i-1
                right=i+1
                while left>=0 and right<l:
                    if s[right]==s[left]:
                        m=left
                        n=right
                        left-=1
                        right+=1
                    else: break
                if n-m>rightPal-leftPal:
                        rightPal=n
                        leftPal=m 
            if s[i]==s[i-1]:
                left=i-1
                right=i
                while left>=0 and right<l:
                    if s[right]==s[left]:
                        m=left
                        n=right
                        left-=1
                        right+=1
                    else:  break 
                if n-m>rightPal-leftPal:
                        rightPal=n
                        leftPal=m
            i=i+1             
        return s[leftPal:rightPal+1]
```

## python3 solution
```python3
class Solution:
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        #超时了
        if not s:return s
        def isPalindrome(left,right):
            i=left
            j=right
            while i<j:
                if s[i]!=s[j]:
                    return False
                i+=1
                j-=1
            return True   
        l=len(s)
        left=0
        right=l-1
        leftPal=0
        rightPal=0
        while left<l:
            right=l-1
            while left<right:
                if s[left]==s[right]:
                    if isPalindrome(left,right):
                        if right-left>rightPal-leftPal:
                            rightPal=right
                            leftPal=left
                        break
                right-=1            
            left+=1            
        return s[leftPal:rightPal+1]     
```

## c solution
```c
//注意 如果lo hi写到函数外面 则在提交时如果上一次的hi-lo大于本次的,则会继续使用上一次的值 所以会出现错误
void expand(char* s,int a,int b,int len,int *lo,int *hi)
{
    int left=a,right=b;
    int m=0,n=0;
    while(left>=0&&right<len)
    {  
        if(s[left]==s[right])
        {
            m=left;
            n=right;
            left--;
            right++;
        } 
        else break;
    }
    if(*hi-*lo<n-m)
    {
        *hi=n;
        *lo=m;
    }
    
}
char* longestPalindrome(char* s) {
    int len=strlen(s);
    int lo=0,hi=0;
    if(len < 2) return s;
    for(int i=0;i<len-1;i++)
    {
        //分别讨论回文字符串长度为偶数和奇数的情况
        expand(s,i,i,len,&lo,&hi);
        expand(s,i,i+1,len,&lo,&hi);
    }  
    
    char *sub=(char*)malloc(sizeof(char)*(hi-lo+2));
    memcpy(sub, s+lo, sizeof(char)*(hi-lo+1));
    sub[hi-lo+1]='\0';
    return sub;
}
```
