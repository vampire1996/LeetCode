# 56. Merge Intervals
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## python solution
```python
# Definition for an interval.
# class Interval:
#     def __init__(self, s=0, e=0):
#         self.start = s
#         self.end = e

class Solution:
    def merge(self, intervals):
        """
        :type intervals: List[Interval]
        :rtype: List[Interval]
        """
        l=len(intervals)
        if l==0:
            return intervals
        res=[]
        Flag=0 #flag=0--未执行 1--本次成功 2--上次成功本次失败 3--上次失败本次失败
        intervals = sorted(intervals, key = lambda x: x.start)
        i=0
        while i<l-1:            
            if intervals[i].end>=intervals[i+1].start and intervals[i].start<=\
              intervals[i+1].end:
              new=Interval(min(intervals[i].start,intervals[i+1].start),max( 
              intervals[i].end,intervals[i+1].end))
              i+=1
              intervals[i]=new
              Flag=1
            elif Flag==1:
              res.append(new)
              Flag=2
              i+=1
            else:
              res.append(intervals[i])
              Flag=3
              i+=1
        res.append(intervals[i])         
        return res
```
