# 139. Word Break
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/139.%20Word%20Break/problem.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/139.%20Word%20Break/example.png"/>

## python solution
```python
"""
DP O(n^2)---1+2+3+...+n
思路整理:
1)res 存储s中每个位置 到该位置能否分裂成wordDict中单词
举个例子：字符串为applepen 和 wordDict为apple，pen。当我们遍历到字母n的时候我们从n开始向前找看看有没有apple：即字符串被分为app和lepen（因为apple
的长度为5，我们期待lepen可能为apple，若lepen确实为apple，app也能够被break（即dp[2] = true)，那么我们将dp[7] = true,但lepen不为apple而且dp[2]为
false，因此我们循环到下一个wordDict即pen，将字符串划分为前面的apple和后面的pen，而后面的pen确实存在，dp[4] = true，所以确实可以划分，因此dp[7]= 
true。
Input: s = "leetcode", wordDict = ["leet", "code"]
      dp  FFFFTFFFT  dp[-1]=True     
"""
class Solution(object):
    def wordBreak(self, s, wordDict):
        res=[False for i in range(len(s)+1)]
        res[0]=True
        for i in range(1,len(s)+1):
            for j in range(i):
                if res[j] and s[j:i] in wordDict:res[i]=True
        return res[len(s)]
```

## python3 solution
```python3
class Solution(object):
    def wordBreak(self, s, wordDict):
        """
        :type s: str
        :type wordDict: List[str]
        :rtype: bool
        """
        dp=[True]
        max_len=max(map(len,wordDict+['']))#找到wordDict中长度最长的单词的长度
        #加['']的目的是避免出现map为空的情况
        words=set(wordDict)#将列表变成集合 这样访问速度变成O(1)
        for i in range(1,len(s)+1):
            #加逗号的原因是使其变成一个元祖(可迭代)
            #这样速度快于dp.append(x)--第二 和dp+=[x]--第三
            dp+=any([dp[j] and s[j:i] in words for j in range(max(0,i-max_len),i)]),
            #不需要遍历i之前的每一个子串 只有[i-max_len,i]范围内的元素才能有可能和words中单词相同
        return dp[-1]
```

## java solution
```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        int max_len=-1;
        for(String word :wordDict)
        {
            max_len=Math.max(max_len,word.length());
        }
        Set<String> words=new HashSet<>(wordDict);
        Queue<Integer> queue = new LinkedList<>();
        queue.add(0);
        boolean[] visited=new boolean[s.length()+1]; 
        /*
        Input: s = "leetcode", wordDict = ["leet", "code"]
        visited     FFFTFFFT
        max_len=4
        leet
         eetc
          etco
           tcod
            code
        */
        while(!queue.isEmpty())
        {
            int start=queue.remove();//弹出列表的第一个元素 FIFO
            for(int end=start+1;end-start<=max_len&&end<=s.length();end++)
            {
                //visited[end]==ture 说明能到达s[end]位置 不需要判断words中是否包含子串
                //当能到达end=s.length()说明成功
                if(end<s.length()&&visited[end]) continue;
                if(words.contains(s.substring(start,end)))
                {
                    if(end==s.length()) return true;
                    queue.add(end);
                    visited[end]=true;
                }
            }
        }
        return false;
    }
}
```
