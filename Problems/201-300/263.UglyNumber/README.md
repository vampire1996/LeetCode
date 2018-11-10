# 263. Ugly Number
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/201-300/263.UglyNumber/problem.png"/>

## c solution
```c
bool isUgly(int num) {
      if(num==0) return false;
      if(num==1) return true;
      while(num!=1)
      {
          if(num%2==0)
          {
              num=num/2;
              continue;
          }
          else if(num%3==0)
          {
              num=num/3;  
              continue;
          }
           else if(num%5==0)
          {
              num=num/5;  
              continue;
          }
          else
          {
              return false;
          }
      }
    return true;
}
```
