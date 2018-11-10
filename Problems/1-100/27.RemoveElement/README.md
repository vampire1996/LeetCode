# 27. Remove Element
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/27.RemoveElement/problem.png "/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/27.RemoveElement/clarification.png "/>

## c solution
```c
int removeElement(int* nums, int numsSize, int val) {
    int len=numsSize;
    for (int i=0;i<numsSize;i++)
    {
        if(nums[i]==val)
        {
            len--;
        }
        else
        {
            nums[i-(numsSize-len)]=nums[i];
        }
    }
    return len;
}
```
