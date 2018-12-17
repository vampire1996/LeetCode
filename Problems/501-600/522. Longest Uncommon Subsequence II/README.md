# 522. Longest Uncommon Subsequence II
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/501-600/522.%20Longest%20Uncommon%20Subsequence%20II/problem.png"/>

## python solution
```python
class Solution:
    def findLUSlength(self, strs):
        """
        :type strs: List[str]
        :rtype: int
        """
        def isSubsequence(s1,s2):
            """
            iter() 函数用来生成迭代器 s会返回s2的下一个值
            if t was '1234' and we check whether '3' is in T = iter(t),
            after we will have next(T) = '4', not '1'
            """
            s=iter(s2)
            """
            all(iterable) returns true if and only if every element of the iterable is truthy.
            也就是说只有s1中每个元素都依次和s2的元素匹配 则s1为s2的子串
            但是要注意["aaa","aaa","aa"]这种情况
            "aa"是"aaa"的子串  "aaa"不是是"aa"的子串
            当s1="aa"  s2="aaa"
            all(c in s2 for c in s1) 为真--因此要用这种写法
            all(c in s1 for c in s2) 为假--s2取到最后一个a时s1已经没有可迭代的元素了
            """
            return all(c in s for c in s1)
        #以字符的长度排序 reverse=True代表长度从大到小--降序
        strs.sort(key=len,reverse=True)
        for s1 in strs:
            """
            如果s1(当前最长的串)不是其他所有串的子串(只是他自己的子串--sum==1)
            则返回其长度即为最长uncommon subsequence
            """
            if sum(isSubsequence(s1,s2) for s2 in strs)==1:
                return len(s1)
        return -1
```

## java solution
```java
class Solution {
    public int findLUSlength(String[] strs) {
         // reverse sorting array with length 
        Arrays.sort(strs,new Comparator<String>()
        {
            public int compare(String s1,String s2)
            {
                //s2.length()-s1.length()--倒序 s1.length()-s2.length()--正序
                return s2.length()-s1.length();
            }
        });
        for(int i=0;i<strs.length;i++)
        {
            int cnt=strs.length-1;
            for(int j=0;j<strs.length;j++)
            {
                if(i!=j&&isSubsequence(strs,i,j)==false)
                    cnt--;
            }
            // strs[i] is not a sub sequence of any other entry
            if(cnt==0)return strs[i].length(); 
        }
        return -1;
    }
    public boolean isSubsequence(String[] strs,int i,int j)
    {
        if(strs[i].length()>strs[j].length())return false;
        int k=0;
        for(char ch:strs[j].toCharArray())
        if(k<strs[i].length()&&ch==strs[i].charAt(k))
        {
            k++;
        }
        return k==strs[i].length();
    }
}
```

