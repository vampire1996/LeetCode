# 90. Subsets II
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## python solution
```python
class Solution(object):
    def subsetsWithDup(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        """
        思路整理:DFS recursion
        1)对nums进行排序以避免nums中重复元素不聚集在一起如[1,2,4,4,3,4]
        2)从nums中依次取出元素加到path中进行DFS
        3)对于重复元素如[1,2,2]中的2，res中每个以2为开头的数组的只取nums的第一个2
        Explanation
        1)sort nums to gather all same number together
        2)take numbers from nums iteratively and use them to conduct DFS
        3)for same numbers like 2 in [1,2,2],each array only take the first 2 as its
        first 2
        """
        def helper(start,end,path,res): 
            res.append(path)
            for i in range(start,end):
                if i!=start and nums[i]==nums[i-1]:continue
                helper(i+1,end,path+[nums[i]],res)
            return
        res=[]
        nums.sort()
        helper(0,len(nums),[],res)
        return res
```

## java solution
```java
/*
对于无重复元素的n维数组 有2^n个子数组 因为每个元素在每个子数组里都只有出现或者不出现两种可能
而对于有重复元素的数组如[1,2,2]
(1)[]
(2)[] [1] 复制一份[] 并向其中加入1
(3)[] [1] [2] [1,2] 复制一份[] [1] 并向其中加入2
(3)[] [1] [2] [1,2] [2,2] [1,2,2]对于重复元素 只向前一次添加过与其相同元素的数组中添加该元素
复制一份[2] [1,2] 并向其中加入2
*/
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> res=new ArrayList<List<Integer>>();
        int start=0;
        res.add(new ArrayList<Integer>());
        Arrays.sort(nums);
        for(int i=0;i<nums.length;i++)
        {
            if(i==0||nums[i]!=nums[i-1]) start=0;
            int size=res.size();
            for(int j=start;j<size;j++)
            {
                List<Integer> temp=new ArrayList<Integer>(res.get(j));
                temp.add(nums[i]);
                res.add(temp);
            }
            start=size;
        }
        return res;
    }
}
```
