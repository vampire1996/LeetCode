# 118. Pascal's Triangle
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/118.PascalsTriangle/problem.png"/>

## c solution
```c
/*int** generate(int numRows, int** columnSizes, int* returnSize) {
    if(!columnSizes) return 0;
    if(!returnSize||numRows==0) return 0;
    int **returnArray=(int **)malloc(numRows*sizeof(int *));
    int *columnSizesArray=malloc(sizeof(int)*numRows);
    
    *returnSize=0;
    int i=0;
    int j=0;
    for(i=0;i<numRows;i++){
           returnArray[i]=(int *)malloc(sizeof(int)*(i+1));
          //columnSizes[i]=(int *)malloc(sizeof(int)*(1));
          columnSizesArray[i]=i+1;
            for(j=0;j<i+1;j++)
            {
                if(j==0) 
                {
                    returnArray[i][j]=1;
                }else if(j==i)
                {
                    returnArray[i][j]=1;
                }else{
                    returnArray[i][j]=returnArray[i-1][j]+returnArray[i-1][j-1];
                }
                
            }
            (*returnSize)++;
            //columnSizes[i][0]=(int)(sizeof(returnArray[i]));
        }
    *columnSizes=columnSizesArray;
    return returnArray;
}*/
/**
 * Return an array of arrays.
 * The sizes of the arrays are returned as *columnSizes array.
 * Note: Both returned array and *columnSizes array must be malloced, assume caller calls free().
 */
int** generate(int numRows, int** columnSizes) {
    int **pascal=(int**)malloc(sizeof(int*) * numRows+1);//分配行的存储空间
     int *columnSizesArray=malloc(sizeof(int)*numRows);
    int j=0,k=0;
    for(int i=0;i<numRows;i++)
    {
        columnSizesArray[i]=i+1;
         pascal[i]=(int*)malloc(sizeof(int)*(i+1)+1);
        for(k=0;k<=i;k++)
        {
            if(k==0||k==i) pascal[i][k]=1;
            else
            {
                pascal[i][k]=pascal[i-1][k-1]+pascal[i-1][k];
            }
        }
       * columnSizes=columnSizesArray;// * columnSizes是有5个指针元素的一维数组
    }
    return pascal;
}
```
