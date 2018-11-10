# 400. Nth Digit
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
int findNthDigit(int n) {
    if(n<10) return n;
    int num=0,bit=0;
    int i=1;
    while(n-9*i*pow(10,i-1)>0)
    {
        num+=9*pow(10,i-1);
        n-=9*i*pow(10,i-1);
        i++;
    }
    num+=n/i;
    bit=n%i;
    if(bit==0) return num%10;
    num++;
    while(num/10)
    {
       if(bit==i) return num%10;
       bit++;
       num/=10;
    }
    return  num%10;
}
```
