# 168. Excel Sheet Column Title
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
//方法1 0ms
 /*   char* convertToTitle(int n) {
    char *a=(char*)malloc(sizeof(char)*26);
    char *Title=NULL;
    int i;
    char j[10000]={0};
    for(i=0;i<26;i++)
    {
        a[i]='A'+i;
        
    }
    i=0;
    while(n/26!=0)
    {
        if(n%26>0)
        {
            j[i]=a[n%26-1];
             n=n/26;
        }
        else
        {
             j[i]=a[25];
             n=n/26-1;
            if(n==0)
            continue;
        }
        i++;  
    } 
    if(n>0)
    {
         j[i]=a[n-1];
    }
    Title=(char*)malloc(sizeof(char)*(i+1));
   for(int k=0;k<=i;k++)
    {
        Title[k]=j[i-k];
    }
    return Title;
}*/
//方法2
char *convertToTitle(int n) {
    char *s;
    int fac = 26, char_size = 0, num = n, i = 1;
    while(num > 0) {
        num = (num - 1) / 26;
        char_size++;
    }
    s=(char*)malloc(char_size*sizeof(char));
    while(n>0){
        n--;//每次计算n都减1 
        *(s+char_size-i) = (char)(n%fac +'A') + *s;
        n/=fac;
        i++;
    }
    return s;
}

```
