# 532. K-diff Pairs in an Array
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/501-600/532.K-diffPairsInAnArray/problem.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/501-600/532.K-diffPairsInAnArray/example.png"/>

## c solution
```c
#define SIZE 1000   //定义Hash table的初始大小
struct HashArray
{
    int key;
    int count;
    struct HashArray *next;
}Hash[SIZE]; //主函数中需要初始化
void addHash(int num)//在Hash table中添加数据
{
    int temp=abs(num%SIZE);//数组中可能有负数
    if(Hash[temp].key==0)
    {
        Hash[temp].key=num;
        Hash[temp].count++;
    }
    else if(Hash[temp].key==num)
    {
        Hash[temp].count++;
    }
    else
    {
         struct HashArray *p=&Hash[temp];
         while(p->next!=NULL&&p->key!=num) {p=p->next;}
         if(p->key==num)  {p->count++;}
         else
          {
              p->next=(struct HashArray *)malloc(sizeof(struct HashArray));
              p=p->next;
              p->key=num;
              p->count=1;
              p->next=NULL;
          }
    }
}
int findHash(int num_temp,int k)
{
    int num=num_temp;
    int temp=abs(num%SIZE);
    if(k==0)
    {
        if(Hash[temp].key==num)
        {
            if(Hash[temp].count==-1) {return 0;}
            if(Hash[temp].count>1) 
            {
                Hash[temp].count=-1;//-1代表相同的数字对只加一次
                return 1;
            }
            Hash[temp].count=-1;
        }
        else
        {
             struct HashArray *p=&Hash[temp];
             while(p->next!=NULL&&p->key!=num) {p=p->next;}
             if(p->key==num)  
             {
                 if(p->count==-1) {return 0;}
                 if(p->count>1) 
                 {
                  p->count=-1;//-1代表相同的数字对只加一次
                  return 1;
                 }
                 p->count=-1;
             }
        }    
        return 0;
    }
    if(Hash[temp].key==num)
    {
        if(Hash[temp].count==-1) return 0;
        Hash[temp].count=-1;
    }
    else
    {
        struct HashArray *p=&Hash[temp];
        while(p->next!=NULL&&p->key!=num) {p=p->next;}
        if(p->key==num)  
        {
          if(p->count==-1) {return 0;}
          p->count=-1; 
         }
    }
    num=num_temp+k;
    temp=abs(num%SIZE);
    if(Hash[temp].key==0&&Hash[temp].count==0) { return 0;}
    if(Hash[temp].key==num&&Hash[temp].count!=0) { return 1;}
    else
    {
        struct HashArray *p=&Hash[temp];
        while(p->next!=NULL&&p->key!=num) {p=p->next;}
        if(p->key==num&&p->count!=0) { return 1;}
        //else return 0;
    }
    return 0;
}
int findPairs(int* nums, int numsSize, int k) {
    int pairs=0;
    if(k<0){return 0;}
    for(int i=0;i<SIZE;i++)
    {
        Hash[i].key=0;
        Hash[i].count=0;
        Hash[i].next=NULL;
    }
    for(int i=0;i<numsSize;i++) { addHash(nums[i]);}
    for(int i=0;i<numsSize;i++)
    {
        if( findHash(nums[i],k)==1) {pairs++;}
    }
    return pairs;
}
//超过限定的存储空间了
/*
int findPairs(int* nums, int numsSize, int k) {
    if(k<0){return 0;}
    int pairs=0,maxNum=INT_MIN,minNum=INT_MAX;
    for(int i=0;i<numsSize;i++)
    {
         maxNum=maxNum>nums[i]?maxNum:nums[i];
         minNum=minNum<nums[i]?minNum:nums[i];
    }
    int *numCount=malloc(sizeof(int)*(maxNum-minNum+1));
        memset(numCount,0,sizeof(int)*(maxNum-minNum+1));
    for(int i=0;i<numsSize;i++)
    {
      numCount[nums[i]-minNum]++;
    }
    for(int i=0;i<maxNum-minNum+1-k;i++)
    {
      if(k==0) {if( numCount[i]>=2){pairs++;}}
      else
      {
          if( numCount[i]!=0&&numCount[i+k]!=0) 
        {
         pairs++;
        }
      }
    }
    free(numCount);
    return pairs;
}*/

```
