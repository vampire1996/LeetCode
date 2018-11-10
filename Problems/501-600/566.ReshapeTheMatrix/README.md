# 566. Reshape the Matrix
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/501-600/566.ReshapeTheMatrix/problem.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/501-600/566.ReshapeTheMatrix/example.png"/>

## c solution
```c
/**
 * Return an array of arrays of size *returnSize.
 * The sizes of the arrays are returned as *columnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */
int** matrixReshape(int** nums, int numsRowSize, int numsColSize, int r, int c, int** columnSizes, int* returnSize) {
    if(numsRowSize*numsColSize!=r*c) 
    {
        int *columnSizesArray=malloc(sizeof(int)*numsRowSize);
        for(int i=0;i<numsRowSize;i++)
        {
        columnSizesArray[i]=numsColSize; 
        }
        *returnSize=numsRowSize;
        * columnSizes=columnSizesArray;
        return nums;
    }
   
    int **returnArray=(int**)malloc(sizeof(int*) * r);//分配行的存储空间
    int *columnSizesArray=malloc(sizeof(int)*r);
    int *nums1D=malloc(sizeof(int)*numsRowSize*numsColSize);
    int k=0;
    for(int i=0;i<numsRowSize;i++)
    {
        for(int j=0;j<numsColSize;j++)
        {
            nums1D[k++]=nums[i][j];
        }
    }
    k=0;
    for(int i=0;i<r;i++)
    {
        returnArray[i]=(int*)malloc(sizeof(int)*c+1);
        columnSizesArray[i]=c; 
         for(int j=0;j<c;j++)
         {
             returnArray[i][j]=nums1D[k++];
         }
    } 
    
    *returnSize=r;
    * columnSizes=columnSizesArray;
    return returnArray;
}
```
