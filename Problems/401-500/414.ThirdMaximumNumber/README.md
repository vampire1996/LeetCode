# 414. Third Maximum Number
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/401-500/414.ThirdMaximumNumber/problem.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/401-500/414.ThirdMaximumNumber/example.png"/>

## c solution
```c
//如果nums中数额差值较大 使用hash需要很大的存储空间 因此会有超时
/*int thirdMax(int* nums, int numsSize) {
    if( numsSize==1) return *nums;
    int numMax=nums[0],numMin=nums[0],cnt=0;
    int thirdNum=0;
    for(int i=1;i<numsSize;i++)
    {
        numMax=numMax>nums[i]?numMax:nums[i];
        numMin=numMin<nums[i]?numMin:nums[i];
    }
    int *hash=malloc(sizeof(int)*(numMax-numMin+1));
    memset(hash,-1,sizeof(int)*(numMax-numMin+1));
    for(int i=0;i<numsSize;i++)
    {
        hash[nums[i]-numMin]++;
    }
    for(int i=numMax-numMin;i>=0;i--)
    {
        if(hash[i]!=-1) cnt++;
         printf("%d\n",cnt);
        if(cnt==3)  
        {
            thirdNum=i+numMin;
            break;
        }
    }
    if(cnt==3) return thirdNum;
    else  return numMax;
}*/
int thirdMax(int* nums, int numsSize) {
    if(numsSize==1) return nums[0];
 int Max1=INT_MIN,Max2=INT_MIN,Max3=INT_MIN;
    bool thirdExist=false;
    for(int i=0;i<numsSize;i++)
    {
        Max1=Max1>nums[i]?Max1:nums[i];
    }
    for(int i=0;i<numsSize;i++)
    {
        if(nums[i]!=Max1)
        Max2=Max2>nums[i]?Max2:nums[i];
    }
     for(int i=0;i<numsSize;i++)
    {
        if(nums[i]!=Max2&&nums[i]!=Max1)  
        {
            Max3=Max3>nums[i]?Max3:nums[i];
           thirdExist=true;
        }
    }
    if(thirdExist) return Max3;
    else return Max1;
}
```
