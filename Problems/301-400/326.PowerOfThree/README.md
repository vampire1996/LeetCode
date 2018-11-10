# 326. Power of Three
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/301-400/326.PowerOfThree/problem.png "/>

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
