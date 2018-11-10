# 189. Rotate Array
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/189.RotateArray/problem.png "/>

## c solution
```c
void rotate(int* nums, int numsSize, int k) {
    k=k%numsSize;
    int j;
    int* num_history=(int*)malloc(sizeof(int)*numsSize);
    for(j=0;j<numsSize;j++)
         {
             num_history[j]=nums[j];
         }
    for(j=0;j<numsSize;j++)
         {
             nums[(j+k)%numsSize]=num_history[j];
         }
}
```
