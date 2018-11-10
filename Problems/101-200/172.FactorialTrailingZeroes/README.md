# 172. Factorial Trailing Zeroes
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/172.FactorialTrailingZeroes/problem.png "/>

## c solution
```c
/*int trailingZeroes(int n) {
    int num=n,cnt=0,returnNum=0;
    while(num)
    {
        num=num/5;
        cnt++;
    }
    for(int i=1;i<cnt;i++)
    {
        returnNum+=n/pow(5,i);
    }
    return returnNum;   
}*/
//修改
int trailingZeroes(int n) {
    int returnNum=0;
    while(n/5)
    {
        returnNum+=n/5;
        n=n/5;
        
    }
    return returnNum;    
}

```
