# 38. Count and Say
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
char* countAndSay(int n) {
    if(n==1) return "1";
     char *s=malloc(sizeof(char)*1+1);
     char *tmp;
     int len,j,cnt,index;
     *s='1';
     *(s+1)=NULL;
    for(int i=1;i<n;i++)
    {
        len=strlen(s);
        tmp=malloc(sizeof(char)*len*2+1);
        memset(tmp, 0, sizeof(char)*len*2+1);
        cnt=1;
        for(j=1,index=0;j<len;j++)
        {
           
           if(s[j]==s[j-1])
           {
               cnt++;
           }
           else
           {
               tmp[index++]='0'+cnt;
               tmp[index++]=s[j-1];
               cnt=1;
           }
        }
        tmp[index++]='0'+cnt;
        tmp[index++]=s[len-1];
        free(s);
        s=tmp;
    }
    return s;
}
```
