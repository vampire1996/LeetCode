# 459. Repeated Substring Pattern
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/401-500/459.%20RepeatedSubstringPattern/problem.png"/>

## c solution
```c
//也可用int memcmp(const void *buf1, const void *buf2, unsigned int count); memcmp是比较内存区域buf1和buf2的前count个字节
bool repeatedSubstringPattern(char* s) {
    int j;
    int len=strlen(s);
    int k;
    for(int i=1;i<=len/2;i++)
    {
        j=i;
        k=0;
        while(j<len)
        { 
            if(len%i!=0) break;
            if(s[k]==s[j])
            {
                j++;
                k++;
            }
            else
            {
                break;
            } 
            if(k==i)
            {
                k=0;
            }
             
        } 
        if(j==len) return true;
    }
    return false;
}
```
