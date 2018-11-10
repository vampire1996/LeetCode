# 28. Implement strStr()
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/28.%20Implement%20strStr/problem.png "/>

## c solution
```c
int strStr(char* haystack, char* needle) {
    int lh = strlen(haystack);
    int ln = strlen(needle);
    
    if((lh == 0 && ln == 0) || ln == 0 || needle == haystack)
      return 0;
    for (int i = 0; i <=(lh-ln); i++) {
        if(haystack[i] == needle[0])
            if(strncmp((haystack+i), needle, ln) == 0)
                return i;
    }
    return -1;
}
/*
//能通过前73个 但最后一个通不过 超时
int strStr(char* haystack, char* needle) {
    if(strlen(needle)==0) return 0;
     if(needle == haystack)
      return 0;
     if(strlen(needle)>strlen(haystack)) return -1;
    int i=0;
    int j=0;
    int k=0;
    int last=-1;
    while(k<strlen(haystack)-strlen(needle)+1)
    {
        i=k;
         while(i<strlen(haystack))
      {
        if(i==last+1)
        {
            if(haystack[i]==needle[j])
            {
            last=i;
            j++;
            }
            else if(haystack[i]==needle[0])
            {
                break;
            }
            else
            {
                j=0;
            }
        }
        else
        {
            if(haystack[i]==needle[j])
            {
            last=i;
            j++;
            }
        }
        if(j==strlen(needle)) return i-strlen(needle)+1;
        i++;

      }
        j=0;
        k++;
    }
    return -1;
}*/
```
