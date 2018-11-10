# 171. Excel Sheet Column Number
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/171.ExcelSheetColumnNumber/problem.png "/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/171.ExcelSheetColumnNumber/example.png "/>

## c solution
```c
int titleToNumber(char* s) {
    int len=strlen(s);
    int num=0;
    for(int i=len-1;i>=0;i--)
    {
        num+=(s[i]-'A'+1)*pow(26,len-1-i);
    }
    return num;
}
```
