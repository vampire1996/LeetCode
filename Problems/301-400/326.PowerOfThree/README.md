# 326. Power of Three
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
bool isPowerOfThree(int n) {
    if(n==0) return false;
    while(n!=1)
    {
        if(n%3==0) n=n/3;
        else return false;
    }
    return true;
}
```
