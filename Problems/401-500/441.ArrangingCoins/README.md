# 441. Arranging Coins
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/401-500/441.ArrangingCoins/problem.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/401-500/441.ArrangingCoins/example.png"/>

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
