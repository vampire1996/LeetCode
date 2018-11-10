# 119. Pascal's Triangle II
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
/**
 * Return an array of size *returnSize.
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* getRow(int rowIndex, int* returnSize) {
    int *returnArray=NULL;
    int *preArray=NULL;
    int i;
    returnArray=(int*)malloc(sizeof(int)*(rowIndex+1));
    preArray=(int*)malloc(sizeof(int)*(rowIndex+1));
    *returnSize=rowIndex+1;
    for(i=0; i<* returnSize;i++)
      {
            returnArray[i]=1;
            preArray[i]=1;
      }
    for(i=0; i<* returnSize;i++)
     {
            for(int j=1;j<i;j++)
            {
                 returnArray[j]=preArray[j]+preArray[j-1];
            }
            for(int l=0;l<* returnSize;l++)
            { 
                preArray[l]=returnArray[l];  
            }
                
    }
    return returnArray;
}
```
