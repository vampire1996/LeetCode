# 78. Subsets
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/74.%20Search%20a%202D%20Matrix/problem.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/74.%20Search%20a%202D%20Matrix/example.png"/>

## python solution
```python
class Solution(object):
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        """
        Input: nums = [1,2,3,4]
        思路整理
        1)每次迭代在res中添加长度比当前最长list长度大1的枚举序列
        2)cur 存储经过一次迭代后res中增加的list数目
          prev 记录上一次迭代res的长度
        3)每次迭代在res中的范围是res[len(res)_previous,len(res)_current]
        4)添加的方法是遍历nums中元素 如果第k个元素索引k大于res[j]最后一个元素在nums中的索引
        则添加该元素
        e.g.
        []---->[1]-------->[1,2] res[0][-1]=1  2,3,4均可添加
                           [1,3]
                           [1,4]
               [2]-------->[2,3] res[1][-1]=2  3,4均可添加
                           [2,4]
               [3]-------->[3,4] res[2][-1]=3  4可添加
               [4]               res[2][-1]=4  无元素可添加
               cur=4 
        Explanation
        each time of iteration,we add one element to all element which has the longest 
        length in res and also they should satisfy following rules:
        res[j][-1]<k    
        k is the index in nums
        j belongs to [len(res)_previous,len(res)_current]
        """
        res=[[]]
        l=len(nums)
        prev=0 
        for i in range(l): 
              temp=prev
              prev=len(res)
              for j in range(temp,len(res)):
                    for k in range(0,l):
                        if temp==0 or k>nums.index(res[j][-1]):
                            """
                            res复制已经存在的元素如res 不能用res.append(res[j])
                            地址传递--修改res[j]的值 会同时改变res[-1]
                            而是应该用下面这种方法 创建一个新的list
                            """
                            res.append([m for m in res[j]])  
                            res[-1].append(nums[k])
        return res
```

## python3 solution
```python3
import functools
"""
reduce把一个函数作用在一个序列[x1, x2, x3...]上，这个函数必须接收两个参数，
reduce把结果继续和序列的下一个元素做累积计算
reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)
"""
class Solution:
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        """
        n取自nums 迭代结果存放于subsets subsets初始化为[[]]
        """
        """
        思路 对于一定长度为n的序列[a,b,c...]有m种子集 则长度为n+1的序列 相当于原序列添加了一个元素
        因此 在原来的子集基础上有两种情况:1)加上这个元素 2)不加这个元素
        因此有2m种子集
        综上 长度为n的序列共有2^n种子集 以下算法的时间复杂度为O(2^n) 与递归的回溯算法相同
        e.g.Input: nums = [1,2,3]
        Initially: [[]]
        Adding the first number to all the existed subsets: [[], [1]];
        Adding the second number to all the existed subsets: [[], [1], [2], [1, 2]];
        Adding the third number to all the existed subsets: [[], [1], [2], [1, 2], [3], [1, 3], [2, 3], [1, 2, 3]].
        """
        return functools.reduce(lambda subsets,n:subsets+[s+[n] for s in subsets],nums,[[]])
```


## java solution
```java
//backtracking --DFS的一种 用于组合排列的问题
/*
回溯算法Input: nums = [1,2,3]
Output:[[],[1],[1,2],[1,2,3],[1,3],[2],[2,3],[3]]
前一个元素的最后一个元素弹出 再加入新的元素
*/
//O(2^n)
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<Integer> list=new ArrayList<Integer>();
        List<List<Integer>> res=new ArrayList<>();
        backTrack(nums,0,list,res);
        return res;
    }
    private void backTrack(int[] nums,int start,List<Integer> list,List<List<Integer>> res)
    {
        res.add(new ArrayList<Integer>(list));
        for(int i=start;i<nums.length;i++)
        {
            list.add(nums[i]);
            backTrack(nums,i+1,list,res);
            list.remove(list.size()-1);
        }
    }
}
```

## c++ solution
```c++
class Solution {
    /*
    Using [1, 2, 3] as an example, 1 appears once in every two consecutive subsets, 2 appears twice in 
    every four consecutive subsets, and 3 appears four times in every eight subsets (initially all 
    subsets are empty)：
    1两个subset一循环 2四个subset一循环 3八个subset一循环
    [], [], [], [], [], [], [], []

    [], [1], [], [1], [], [1], [], [1]

    [], [1], [2], [1, 2], [], [1], [2], [1, 2]

    [], [1], [2], [1, 2], [3], [1, 3], [2, 3], [1, 2, 3]
    */
    //O(n*2^n)
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        //c++中的size()和length()没有区别
        int n=pow(2,nums.size());
        vector<vector<int>> sets(n,vector<int>());
        for(int i=0;i<nums.size();i++)
        {
            for(int j=0;j<n;j++)
            {
                //以2^(i+1)为周期 前2^i不添加元素(最低位为0) 
                if(1&(j>>i))
                {
                    sets[j].push_back(nums[i]);//向量的最后添加元素
                    //后2^i添加元素(最低位为1)
                }
            }
        }
        return sets;
    }
};
```
