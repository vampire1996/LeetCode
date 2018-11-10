# 561.Arrary Partition I
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/501-600/561.ArraryPartition%20I/problem.png "/>

## c solution
```c
//快速排序使用分治策略(Divide and Conquer)来把一个序列分为两个子序列。步骤为：
/*
    从序列中挑出一个元素，作为"基准"(pivot).
    把所有比基准值小的元素放在基准前面，所有比基准值大的元素放在基准的后面（相同的数可以到任一边），这个称为分区(partition)操作。
    对每个分区递归地进行步骤1~2，递归的结束条件是序列的大小是0或1，这时整体已经被排好序了。
*/
void swap(int a[],int i,int j)
{
    int temp;
    temp=a[i];
    a[i]=a[j];
    a[j]=temp;
}
int partition(int a[],int left,int right)// 划分函数
{
    int pivot=a[right];// 这里每次都选择最后一个元素作为基准
    int tail=left-1;// tail为小于基准的子数组最后一个元素的索引
    for(int i=left;i<right;i++)// 遍历基准以外的其他元素
    {
        if(a[i]<=pivot)// 遍历基准以外的其他元素
        {
          swap(a,++tail,i);
        }
    }
    swap(a,tail+1,right); // 最后把基准放到前一个子数组的后边，剩下的子数组既是大于基准的子数组
    // 该操作很有可能把后面元素的稳定性打乱，所以快速排序是不稳定的排序算法
    return tail+1;// 返回基准的索引
}
void QuickSort(int a[],int left,int right)
{
    if(left>=right) return;             
    int pivotIndex=partition(a,left,right);  // 基准的索引
    QuickSort(a,left,pivotIndex-1);         
    QuickSort(a,pivotIndex+1,right);
}
int comp(const void*a,const void*b)
{
return *(int*)a-*(int*)b;//a-b是从小到大排序  b-a是从大到小排序
}
/oid qsort(void*base,size_t num,size_t width,int(__cdecl*compare)(const void*,const void*));
//冒泡排序太慢O(n^2) 使用快速排序O*(nlogn)
int arrayPairSum(int* nums, int numsSize) {
    int sum=0,temp;
     QuickSort(nums,0,  numsSize-1);
    //qsort(nums,numsSize,sizeof(int),comp);//也可以直接用快速排序库函数
    for(int i=0;i<numsSize;i+=2)
    {
        sum+=nums[i];
    }
    return sum;    
}
```
