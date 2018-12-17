# 134. Gas Station
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/134.%20Gas%20Station/problem.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/134.%20Gas%20Station/example.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/134.%20Gas%20Station/example2.png"/>

## python solution
```python
class Solution(object):
    def canCompleteCircuit(self, gas, cost):
        """
        :type gas: List[int]
        :type cost: List[int]
        :rtype: int
        """
        """
        思路整理:
        1)如果sum(gas+cost)>=0 一定有方案可以从某一位置出发回到该位置
        证明:
        i.假设下面部分和为最小
        gas[0]-cost[0]+gas[1]-cost[1]+...+gas[i]-cost[i]
        ii.则开始位置为start=i+1 且满足gas[i+1]-cost[i+1]>=0
        (若gas[i+1]-cost[i+1]<0,则0-i不是最小)
         以下各不等式均应该满足 --也就是能从i+1到最后
         gas[i+1]-cost[i+1]>=0
         gas[i+1]-cost[i+1]+gas[i+2]-cost[i+2]>=0
         .......
         gas[i+1]-cost[i+1]+gas[i+2]-cost[i+2]+...+gas[n-1]-cost[n-1]>=0
         (从i+1到之后的任意一个位置均应该大于等于0,若小于0 则则0-i不是最小)
         同时有(因为从0-i之和为最小 任何j<i均满足下列不等式)
         gas[0]-cost[0]+gas[1]-cost[1]+...+gas[j]-cost[j] + gas[i+1]-cost[i+1]+...+gas[n-1]-cost[n-1]
         >=
         gas[0]-cost[0]+gas[1]-cost[1]+...+gas[i]-cost[i] + gas[i+1]-cost[i+1]+...+gas[n-1]-cost[n-1]=sum(gas+cost)
         >=0
         由上可知
         gas[i+1]-cost[i+1]>=0,
         gas[i+1]-cost[i+1]+gas[i+2]-cost[i+2]>=0,
         gas[i+1]-cost[i+1]+gas[i+2]-cost[i+2]+...+gas[n-1]-cost[n-1]>=0,
         ...
         gas[i+1]-cost[i+1]+...+gas[n-1]-cost[n-1] + gas[0]-cost[0]+gas[1]-cost[1]+...+gas[j]-cost[j]>=0,
         ...
         从i+1出发可以到达0-i的任意一个位置
         得证

        """
        tank,total,start=0,0,0
        for i in range(len(gas)):
             tank=tank+gas[i]-cost[i]
             if tank<0:
                    total+=tank
                    tank=0
                    start=i+1
        return -1 if tank+total<0 else start
```

## java solution
```java
class Solution {
    /*
    思路整理:贪心算法
    从start开始走尽可能远的位置(sum>=0) 当无法再前进(sum<0)start向后退一位 也就是从新的位置开始出发
    当start与end相遇 则可从start出发回到该位置(前提sum>=0)
    */
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int start=gas.length-1,end=0;
        int sum=gas[start]-cost[start];
        while(start>end)
        {
            if(sum>=0)
            {
                sum+=gas[end]-cost[end];
                end++;
            }
            else
            {
                start--;
                sum+=gas[start]-cost[start];
            }   
        }
        return sum>=0?start:-1;
    }
}
```
