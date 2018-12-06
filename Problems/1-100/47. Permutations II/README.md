# 47. Permutations II
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/46.Permutations/problem.png"/>

## python solution
```python
class Solution(object):
    def permuteUnique(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        """
        思路整理
        1)对nums进行排序 
        2)遍历nums 当输入为11111112 只取最后一个1作为path的首元素 则12111111只会在res中出现一次
        3)递归调用helper以去除遍历到的元素剩下的nums中元素为输入
        4)注意遍历结束后还要记得最后一个元素也要将其递归
        Explanation
        1)sort nums
        2)traverse nums when the input is like 11111112,only take the last 1 as the first 
        number of path,so 12111111 only appears in res for one time
        3)recursively use helper with the resevation of nums without nums[i]
        4)to be noticed,after traversion,we should consider the last element of nums
        """
        def helper(array,path,res):
            if not array:
                res.append(path)
                return
            l=len(array)
            if l==1:
                helper([],path+[array[0]],res)
                return
            for i in range(l-1):
                if array[i]!=array[i+1]:
                     helper(array[:i]+array[i+1:],path+[array[i]],res)
            helper(array[:l-1],path+[array[l-1]],res)
        res=[]
        if not nums:return nums
        nums.sort()
        helper(nums,[],res)
        return res     
```

## python3 solution
```python3
class Solution:
    def permuteUnique(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        """
        思路整理
        1)对于123456 插入一个数 有len(123456)+1=7个插入位置
        i.若插入n==7与之前元素无重复(123456+[7]).index(7)+1=7 则有7个插入位置
        ii.若插入n==3与之前元素有重复(123456+[3]).index(3)+1=3 则有3个插入位置
        也就是说只能在123的3之前插入 之后插入的话如1234356 会和124356插入3的情况重复
        """
        res=[[]]
        for n in nums:
            res=[rest[:i]+[n]+rest[i:] for rest in res for i in range((rest+[n]).index(n)+1)]
        return res
```

## c++ solution
```c++
class Solution {
public:
    /*值得注意的是recursion中num为值传递而不是地址传递&num
    对于Input: [1,1,2] 当迭代至i=1 k=2时 会将num[1] nums[2]交换nums[2]=1
    而i=0,k=2时 我们希望nums[2]=2而不是1，一次每次递归传递的是num交换后的值
    而原num在递归调用recursion时并不会改变
    */
    void recursion(vector<int> num, int i, int j, vector<vector<int> > &res) {
        if (i == j-1) {
            res.push_back(num);
            return;
        }
        for (int k = i; k < j; k++) {
            if (i != k && num[i] == num[k]) continue;
            swap(num[i], num[k]);
            recursion(num, i+1, j, res);
        }
    }
    vector<vector<int> > permuteUnique(vector<int> &num) {
        sort(num.begin(), num.end());
        vector<vector<int> >res;
        recursion(num, 0, num.size(), res);
        return res;
    }
};
```

## java solution
```java
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        
        if (nums==null)return res;
        Arrays.sort(nums);
        helper(nums,0,nums.length,res);
        return res;
        
    }
    public void helper(int[] nums,int i,int j,List<List<Integer>> res)
    {
        if(i==j-1)
        {
            List<Integer> li = new ArrayList<Integer>();
            for(int m=0;m<nums.length;m++)li.add(nums[m]);
            res.add(new ArrayList<Integer>(li));
            return;
        }
        
         for (int k = i; k < j; k++) {
            if (i != k && nums[i] == nums[k]) continue;
            swap(nums,i, k);
            //需要调用Arrays.copyOf()新建一个实例，这样递归调用是就不会修改原nums的值
            helper(Arrays.copyOf(nums,nums.length), i+1, j, res);   
        }
    }
    private void swap(int[] nums, int i, int j) {
        int save = nums[i];
        nums[i] = nums[j];
        nums[j] = save;
    }
}
```
