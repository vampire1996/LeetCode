# 344. Reverse String
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/301-400/345.ReverseVowelsofAString/problem.png "/>

## c solution
```c
char* reverseString(char* s) {
    int n=strlen(s);//strlen最好只用一次 降低计算时间
     char* returnArray = malloc(sizeof(char) *(n + 1));
    for(int i=0;i<n;i++)
    {
        returnArray[i]=s[n-1-i];
    }
    returnArray[n]='\0';//'\0'和NULL等价
    return returnArray;
}
```
