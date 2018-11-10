# 7. 88. Merge Sorted Array
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
void merge(int* nums1, int m, int* nums2, int n) {
    for(int i=m-1,j=n-1,k=m+n-1;j>=0;)
    {
        nums1[k--]=i>=0&&nums1[i]>nums2[j]?nums1[i--]:nums2[j--];
    }
}
```
