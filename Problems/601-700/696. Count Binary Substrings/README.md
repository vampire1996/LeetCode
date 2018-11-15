# 696. Count Binary Substrings
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/46.Permutations/problem.png"/>

## python solution
```python
class Solution:
  def countBinarySubstrings(self, s):
        """
        将S中所有形如10 01片段截断 并利用len函数计算每一段的长度
        """
        s = list(map(len, s.replace('01', '0 1').replace('10', '1 0').split()))
        """
        map() 会根据提供的函数对指定序列做映射。
        map(function, iterable, ...)
        此处为计算字符串的长度
        
        replace() 方法把字符串中的 old（旧字符串） 替换成 new(新字符串)
        
        Python split() 通过指定分隔符对字符串进行切片
        str -- 分隔符，默认为所有的空字符，包括空格、换行(\n)、制表符(\t)等。
        
        
        """
        """
        s中存放连续的0或1的长度
        如s=[2 3 4 5 6]
          s[1:]=[3 4 5 6]
          则min(a, b)表示取出相邻两个0序列和1序列的最小者并叠加到sum上去
        """
        return sum(min(a, b) for a, b in zip(s, s[1:]))
        """
        zip() 函数用于将可迭代的对象作为参数，将对象中对应的元素打包成一个个元组，然后返回由这些元组组成的列表。
        >>>a = [1,2,3]
        >>> b = [4,5,6]
        >>> zipped = zip(a,b)     # 打包为元组的列表
        [(1, 4), (2, 5), (3, 6)]
        """
```
## c solution
```c
int min(int a,int b)
{
    return a>b?b:a;
}
int countBinarySubstrings(char* s) {
    int l=strlen(s);
    int cnt=0,pre=0,cur=1;
    for(int i=1;i<l;i++)
    {
        if(s[i]==s[i-1])
        {
            cur++;
        }
        else
        {
            cnt+=min(cur,pre);
            pre=cur;
            cur=1;
        }
    }
    
    return cnt+min(cur,pre);
}

```
