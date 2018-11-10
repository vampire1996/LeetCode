# 167. Two Sum II - Input array is sorted
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
/**
 * Return an array of size *returnSize.
 * Note: The returned array must be malloced, assume caller calls free().
 */
/*int* twoSum(int* numbers, int numbersSize, int target, int* returnSize) {
    int i = 0, j = numbersSize -1;
    int* returnArray = NULL;
    while(i<numbersSize && j>=0){
      printf("%d ",i);
        if(numbers[i] + numbers[j] > target) j--;
        else if(numbers[i] + numbers[j] < target) i++;
        else{
            *returnSize = 2;
            returnArray = malloc((*returnSize) * sizeof(int));
            returnArray[0] = i+1; // +1 required by example
            returnArray[1] = j+1;
            return returnArray;
        }
    }
    return returnArray;
}*/

int* twoSum(int* numbers, int numbersSize, int target, int* returnSize) {
    int *returnArray=NULL;
    int i=0;
    int j;
    for(i;i<numbersSize-1;i++)
    {
        for(j=i+1;j<numbersSize;j++)
        { 
            if((numbers[j]+numbers[i])!=target)
            {
                continue;
            } 
            else
            {
                * returnSize=2;
                returnArray=(int*)malloc(sizeof(int)*( * returnSize));
                returnArray[0]=i+1;
                returnArray[1]=j+1; 
                return returnArray;
            }
            
        }
        
    }
     return returnArray;
    
}
```
