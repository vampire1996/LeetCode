# 58. Length of Last Word
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/58.LengthofLastWord/problem.png"/>

## c solution
```c
int lengthOfLastWord(char* s) {
    int i;
    int j=0;
    int k=0;
    for(i=0;i<strlen(s);i++)
    {
        if(s[strlen(s)-i-1]!=' ')//也可以用isspace（*s）函数判断字符是否为空
        {
        j=strlen(s)-i;//算出去除句尾空格后的字符串长度
        break;
        }
    }
    for(i=0;i<j;i++)
    {
       if(s[j-i-1]!=' ')
           ++k;
        else
            break;
    }
    return k;
}
```
