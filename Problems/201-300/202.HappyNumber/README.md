# 202. Happy Number
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
bool isHappy(int n) {
    int num=n;
    int sum=0;
    for(int i=0;i<5;i++)
    {
         while(num!=0)
       {
        sum+=pow(num%10,2);
        num=num/10;
       }
        if(sum==100||sum==10||sum==1) return true;
        num=sum;
        sum=0;
    }
    return false;
}
//方案2 Using fact all numbers in [2, 6] are not happy (and all not happy numbers end on a cycle that hits this interval):
/*
bool isHappy(int n) {
    while(n>6){
        int next = 0;
        while(n){next+=(n%10)*(n%10); n/=10;}
        n = next;
    }
    return n==1;
}
*/
```
