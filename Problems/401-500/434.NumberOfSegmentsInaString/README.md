# 434. Number of Segments in a String
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
int countSegments(char* s) {
    if(s==NULL) return 0;
    int len=strlen(s);
    int count=0;
    char preString=s[0];
    for (int i=i;i<len;i++)
    {
        if(s[i]!=' '&&preString==' ') count++;
        preString=s[i];
    } 
    if(count!=0)
    {
          if(s[0]!=' ')
        {
          return count+1;  
        }
         else
        {
          return count;
        }
    }    
    else 
    {
       if(s[0]!=' '&&s[0]!=NULL) return count+1;
         else return 0; 
    } 
}
```
