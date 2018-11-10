# 521. Longest Uncommon Subsequence I 
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
int findLUSlength(char* a, char* b) {
    if(a[0]==NULL&&b[0]==NULL) return -1;
    int n1=strlen(a),n2=strlen(b);
    if(a[0]!=NULL&&b[0]==NULL) return n1;
    if(a[0]==NULL&&b[0]!=NULL) return n2;
    if(n1!=n2) return n1>n2?n1:n2;
    for(int i=0,j=0;i<n1,j<n1 ;i++,j++ )
    {
      if(a[i]!=b[j]) 
      {
         return n1;
      }
    }
     return -1;
}
```
