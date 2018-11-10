# 367. Valid Perfect Square
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

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
