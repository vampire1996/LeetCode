# 198. House Robber
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/198.%20House%20Robber/problem.png "/>

## c solution
```c
int min(int a,int b)
{
    return a<b?a:b;
}
//c solution 72ms
int max1(int a,int b)
{
    return a>b?a:b;
}
int maxArea(int* height, int heightSize) {
    int i=0,j=heightSize-1;
    int max=min(height[i],height[j])*(j-i);
    int temp1=height[j],temp2=height[i];
    while(j>0)
    {
        if(height[j]>temp1||j==heightSize-1)//比之后最大高度大则进行计算
        while(i<j)
       {
        if(height[++i]>temp2)//比之前最大高度大则进行计算
            max=max1(min(height[i],height[j])*(j-i),max);
        }
        i=0;
        temp1=max1(height[j],temp1);
        temp2=max1(height[i],temp2);
        max=max1(min(height[i],height[--j])*(j-i),max);
    }
    return max;
}
```
## c solution
```python
#python solution 36ms
class Solution(object):
    def maxArea(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        mx_quantity = -1
        i = 0
        j = len(height) - 1
        while i < j:
            mn = min(height[i], height[j])
            
            cur_quantity = mn * (j-i)
            if cur_quantity > mx_quantity:
                mx_quantity = cur_quantity
            
            if mn == height[i]:#左边和右边高度谁小在谁那边步进一个单位
                i+=1
            else:
                j -= 1
        
        return cur_quantity if cur_quantity > mx_quantity else mx_quantity
```
