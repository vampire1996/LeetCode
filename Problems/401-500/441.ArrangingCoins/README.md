# 441. Arranging Coins
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
int arrangeCoins(int n) {
    int rows=0;
    int width=1;
    while(n>=0)
    {
        n-=width;
        width++;
        rows++;
    }
    return rows-1;
}
```
