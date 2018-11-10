# 231. Power of Two
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/201-300/231.PowerOfTwo/problem.png "/>

## c solution
```c
bool isPowerOfTwo(int n) {
    if(n==0) return false;
    while(n!=1)
    {
        if(n%2!=0) return false;
        else
        {
            n=n/2;
        }
    }
    return true;
}

```
