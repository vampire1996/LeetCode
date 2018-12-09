# 40. Combination Sum II
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## python solution
```python
class Solution(object):
    def combinationSum2(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        """
        Input: candidates = [10,1,2,7,6,1,5], target = 8
        思路整理
        1)对 candidates排序--candidates = [1,1,2,5,6,7,10]
        2)递归执行
        i.遍历已排序的数组 如果和之前计算结果(n)之和为target 则加入res 
        ii.如果和小于target 则递归调用helper并将计算结果加入当前遍历到的数
        iii.如果和大于于target 由于数组是排序的 当前元素之后的元素只能更大，因此返回
        3)注意，每次递归只取数组中的一个数和之前计算结果相加，当遇到重复元素只取最前面的一个
        Explanation
        1)sort candidates
        2)conduct recursively
        i.if candidates[i]+n==target thus we add path to res
        (n represents the previous sum of certain numbers before candidates[i])
        ii.if candidates[i]+n<target,call the helper recursively andadd candidates[i] to n
        iii.if candidates[i]+n<target,because our array is sorted,so the elements after 
        is larger than candidates[i],it's a waste of time to traversal them,so we just return
        3)To be noticed,we only take one element in candidates[i] each time,so we just 
        skip the duplicates after the first one 
        """
        def helper(res,nums,path,n):
            if not nums:return
            for i in range(len(nums)):
                if i!=0 and nums[i]==nums[i-1]:continue
                if nums[i]+n==target:
                    res.append(path+[nums[i]])
                    break
                elif nums[i]+n<target:
                    helper(res,nums[i+1:],path+[nums[i]],n+nums[i])
                else:return
        candidates.sort()
        res=[]
        helper(res,candidates,[],0)
        return res
```

## python solution
```python
//BFS--backtrack
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> res=new ArrayList<>();
        List<Integer> path=new ArrayList<Integer>();
        Arrays.sort(candidates);
        backtrack(candidates,res,target,path,0);
        return res;
    }
    private static void backtrack(int[] candidates,List<List<Integer>> res,int remain,List<Integer> path,int start)
    {
        if(candidates==null)return;
        if(remain==0)
        {
            res.add(new ArrayList(path));
            return;
        }
        for(int i=start;i<candidates.length;i++)
        {
            if(i!=start&&candidates[i]==candidates[i-1])continue;
            if(remain-candidates[i]<0)break;
            path.add(candidates[i]);
            backtrack(candidates,res,remain-candidates[i],path,i+1);
            path.remove(path.size()-1);
        }
    }
}
```

