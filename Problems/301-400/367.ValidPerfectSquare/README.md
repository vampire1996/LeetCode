# 367. Valid Perfect Square
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/301-400/367.ValidPerfectSquare/problem.png"/>

## c solution
```c
//二分法相当于牛顿法中X0为mid=(left+right)/2
bool isPerfectSquare(int num) {
    int left=1,right=num;
    int mid=(left+right)/2;
    while(1)
    {
        if(num/mid>mid)
        {
            if(num/mid-mid==1) break;
            left=mid;
            mid=(left+right)/2;
        }
        else if(num/mid<mid)
        {
            if(mid-num/mid==1) break;
            right=mid;
            mid=(left+right)/2;
        }
        else
        {
            if(mid*mid==num) return true;
            else return false;
        }
    }
    return false;
}
```
