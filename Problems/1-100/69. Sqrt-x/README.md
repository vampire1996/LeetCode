# 69. Sqrt(x)
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/69.%20Sqrt-x/problem.png "/>

## c solution
```c
/*
int mySqrt(int x) {
    if(x<=1) return x;
    for(int i=1;i<x;i++)
    {
        if(i*i==x) return i;
        else if(pow(i,2)<x&&pow(i+1,2)>x)
        {
            return i;
        }
    }
    return 0;
}*/
//binary search
int mySqrt(int x) {
    if(x<=1) return x;
    int left=1,right=x,mid=(left+right)/2;
    while(1)
    {
        if(x/mid>mid)
        {
            if(x/mid-mid==1) return mid;
            left=mid;
            mid=(left+right)/2;
        }
        else if(x/mid<mid)
        {
            if(mid-x/mid==1) return x/mid;
            right=mid;
            mid=(left+right)/2;
        }
        else return mid;
    }
    return 0;
}
```
