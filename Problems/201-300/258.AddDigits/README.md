# 258. Add Digits
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/201-300/258.AddDigits/problem.png "/>

## c solution
```c
int addDigits(int num) {
    if(num<10) return num;
    int sum=0;
    while(num>=10)
    {
       while(num)
       {
        sum+=num%10;
        num=num/10;
       } 
        num=sum;
        sum=0;
    }
     return num;
}
```
