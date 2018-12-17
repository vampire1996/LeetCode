# 539. Minimum Time Difference
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## python solution
```python
class Solution(object):
    def findMinDifference(self, timePoints):
        """
        :type timePoints: List[str]
        :rtype: int
        """
        """
        思路整理:
        1)对所有时间点排序 找到排序后所有相邻时间点间最小的时间差 
        注意还有第一个和最后一个也是相邻的
        2)计算两个时间点的最小时间差
        i.s1-s2>12h diff=(23-hour2+hour1)*60+60-min2+min1
        ii.s1-s2<=12h diff=(hour2-hour1)*60+min2-min1
        explanation
        1)sort all time points,find the minimun difference between all adjacent
        time points
        to be noticed,the first and the last are also adjacent
        2)calculate the diffenence between two adjacent
        time points 
        """
        def calDiff(s1,s2):
            hour1=(ord(s1[0])-ord('0'))*10+ord(s1[1])-ord('0')
            hour2=(ord(s2[0])-ord('0'))*10+ord(s2[1])-ord('0')
            min1=(ord(s1[3])-ord('0'))*10+ord(s1[4])-ord('0')  
            min2=(ord(s2[3])-ord('0'))*10+ord(s2[4])-ord('0')
            if hour2-hour1>12 or (hour2-hour1==12 and min1<min2) :
                return (23-hour2+hour1)*60+60-min2+min1
            else: return (hour2-hour1)*60+min2-min1
        timePoints.sort()#升序排列
        diff=calDiff(timePoints[0],timePoints[-1])
        for i in range(len(timePoints)-1):
            diff=min(diff,calDiff(timePoints[i],timePoints[i+1]))
        return diff
```

## python3 solution
```python3
class Solution:
    def findMinDifference(self, timePoints):
        """
        :type timePoints: List[str]
        :rtype: int
        """
        def convert(s):
            return int(s[0:2])*60+int(s[3:])
        """
        map()是 Python 内置的高阶函数，它接收一个函数 f 和一个 list，
        并通过把函数 f 依次作用在 list 的每个元素上，得到一个新的 list 并返回。
        """
        minutes=list(map(convert,timePoints))
        minutes.sort()
        """
        zip() 函数用于将可迭代的对象作为参数，将对象中对应的元素打包成一个个元组，然后返回由这些元组组成的列表
        下面zip(minutes,minutes[1:]+minute[0])的含义是
        返回[(mintues[0],mintues[1]),(mintues[1],mintues[2]),...(mintues[n-1],mintues[0])]
        对应元素依次相减
        """
        """
        对于相邻时间点 都有两个时间差 min1-min2 和24*60-min1+min2
        对于升序排列的两个相邻时间点其24*60-min1+min2 一定大于首元素和末元素 24*60-first+last
        因此只需计算min1-min2%(24*60)=min1-min2>0
        对于首元素和末元素 24*60-first+last
        first-last<0 如0-1439=-1439
        而-1439%(24*60)=1 即为我们想要的结果
        """
        """
        -9%7=-9 - 7*[-2]=5
         9%-7=-9 - -7*[-2]=-5
        """
        return min((y-x)%(24*60) for x,y in zip(minutes,minutes[1:]+minutes[:1]))
```

## java solution
```java
class Solution {
    public int findMinDifference(List<String> timePoints) {
        //因为时间点一共有24*60个 将其转换为24*60个布尔型变量 
        //若在timePoints中出现 则在对应位置置为true
        //接下来计算timePoints中相邻时间点的差值的最小值
        //同时 将最后的min与时间点的最小值与最大值的差60*24-(last-first)比较 找到二者间的最小值
        //不能是last-fast 因为任意相邻的两个时间点都比它小
        boolean[] mask=new boolean[24*60];
        for(String time:timePoints)
        {
            //praseInt() 返回值为int对象 
            //valueOf()返回值为Integer，可以使用Integer对象里面的所有方法，
            //包括转为Object对象，而int类型不能转为Object对象
            String[] t=time.split(":");
            
             int hour = Integer.parseInt(t[0]);
            int Min=Integer.parseInt(t[1]);
            if(mask[hour*60+Min]) return 0;
            mask[hour*60+Min]=true;
        }
        int min=Integer.MAX_VALUE,first=Integer.MAX_VALUE,last=Integer.MIN_VALUE,pre=Integer.MAX_VALUE;
        for(int i=0;i<60*24;i++)
        {
            if(mask[i])
            {
                if(first!=Integer.MAX_VALUE)
               {
                min=Math.min(min,i-pre);
               }
                
                first=Math.min(i,first);
                last=Math.max(i,last);
                pre=i; 
            }
        }
        min=Math.min(min,60*24-(last-first));
        return min;
    }
}
```
