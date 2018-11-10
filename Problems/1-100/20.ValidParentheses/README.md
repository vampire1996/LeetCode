# 20. Valid Parentheses
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/20.ValidParentheses/problem.png "/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/20.ValidParentheses/example.png "/>

## c solution
```c
bool isValid(char* s) {
    if(strlen(s)%2!=0) return false;
    char *map=(char*)malloc(sizeof(char)*(strlen(s)/2));
    int a[126]={0};
    a['(']=1;
    a['{']=1;
    a['[']=1;
    a[')']='(';
    a['}']='{';
    a[']']='[';
    int count=0;
    for(int i=0;i<strlen(s);i++)
    {
        if(a[s[i]]==1) map[count++]=s[i];
        else
        {
            if(count>0&&a[s[i]]==map[count-1]){count--;}
            else 
                return false;
        }
       // if(count>strlen(s)/2)   return false;
    }
    if(count>0) return false;
    return true;
}

```
