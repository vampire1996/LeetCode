# 169. Majority Element
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/169.MajorityElement/problem.png"/>

## c solution
```c
int majorityElement(int* nums, int numsSize) {  
    int count[numsSize/2+1];//在C中，使用变量来定义数组长度是，这个数组可以定义，却不能进行初始化赋值，可以在之后赋值。
    int nums_I[numsSize/2+1];
    for(int i=0;i<numsSize/2+1;i++)
    {
        count[i]=0;
    }
    nums_I[0]=nums[0];
    count[0]=1;
    int num_count=1;
    for (int i=1;i<numsSize;i++)
    {
       for(int j=0;j<num_count;j++)
       {
           if(nums[i]!=nums_I[j])  
           {
              
           }
           else
           {
              count[j]++;
               break;
           }
           if(j==num_count-1) 
           {
               nums_I[num_count++]=nums[i];
           }
       }
    }
    for(int i=0;i<num_count;i++)
    {
        if(count[i]>numsSize/2) return nums_I[i];
    }
    return 0;
}

```
