# 258. Add Digits
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

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
