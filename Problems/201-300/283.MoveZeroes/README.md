# 283. Move Zeroes
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/201-300/283.MoveZeroes/problem.png "/>

## c solution
```c
void moveZeroes(int* nums, int numsSize) {
          int zeroSize=0;
          for(int i=0;i<numsSize;i++)
          {
               if(nums[i]==0)
               {
                   zeroSize++; 
               }
              else
              {
                   nums[i-zeroSize]=nums[i];
              }
          }
         for(int i=0;i<zeroSize;i++)
         {
              nums[numsSize-i-1]=0;
         }     
}
```
