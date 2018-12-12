# 91. Decode Ways
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/106.%20Construct%20Binary%20Tree%20from%20Inorder%20and%20Postorder%20Traversal/problem.png"/>

## python solution
```python
class Solution:
    def numDecodings(self, s):
        """
        :type s: str
        :rtype: int
        """
        """
        思路整理:
        1)用cnt[len(s)]存储截止到s[i](包括s[i])所有可能的编码数
        2)对于任意s[i] 
         i.若 '1'<=s[i]<='9' 则s[i]都可以直接单独加到之前的编码队列--cnt[i-1]
            同时,若s[i-1]=='1' 或者 s[i-1]=='2' and '1'<=s[i]<='6'
            则s[i],s[i-1]二者可以结为1个编码 但前提是s[i-1]未与s[i-2]结合
            此时我们用twoDigits记录之前的编码队列的s[i-1]与s[i-2]结合成的两位数
            cnt[i-1]-twoDigits即为s[i-1]未与s[i-2]结合的数目--temp
            则cnt[i]=cnt[i-1]+temp
            同时temp可作为下一次迭代时的twoDigits
         ii.若 's[i]=='0' s[i]只能和s[i-1]结为1个编码
            因此,cnt[i]=temp
        Explanation
        1)we use cnt[len(s)] to store all possible decode ways up to s[i](include s[i])
        2)for every s[i]
        i.if '1'<=s[i]<='9'
          s[i] can add the formal decoding list seprately--cnt[i-1]
          meanwhile,if s[i-1]=='1' or(s[i-1]=='2' and '1'<=s[i]<='6')
          we can combine s[i] with s[i-1] to one number but we should ensure that s[i-1]
          and s[i-2] are not combined
          we use twoDigits to represent the number of combinations between s[i-1]
          and s[i-2],so cnt[i-1]-twoDigits is the number of which s[i-1] and s[i-2] are 
          not combined
          so cnt[i]=cnt[i-1]+temp
          to be noticedw,temp can the next twoDigits
        ii.if 's[i]=='0' s[i] can one combines with s[i-1]
           thus cnt[i]=temp
        """
        if not s or s[0]=='0':return 0
        l=len(s)
        last=s[0]
        twoDigits=0
        cnt=[0 for i in range(l)]
        cnt[0]=1
        for i in range(1,l):
            #连续两个0 或者0之前为一大于2的数
            if s[i]=='0' and (last=='0' or ord(last)>ord('2')):
                return 0
            if last=='1':temp=cnt[i-1]-twoDigits
            elif last=='2' and ord(s[i])<ord('7'):temp=cnt[i-1]-twoDigits
            else:temp=0
            cnt[i]=cnt[i-1]+temp if s[i]!='0' else temp
            twoDigits=temp
            last=s[i]
        return cnt[l-1]
```
## java solution
```java
class Solution {
    public int numDecodings(String s) {
        if(s==null)return 0;
        int l=s.length();
        int dp[]=new int[l];
        //dp[l]每个元素均初始化为0
        dp[0]=s.charAt(0)=='0'?0:1;
        //对于000123这种情况 由于dp[0:2]均为0 因此dp[3:5]也均为0--dp[i]+=dp[i-1/2];
        for(int i=1;i<l;i++)
        {
            /*
            public String substring(int beginIndex, int endIndex)  左闭右开
            第一个int为开始的索引，对应String数字中的开始位置，--能取到
            第二个是截止的索引位置，对应String中的结束位置--取不到
            */
            /*
            Integer.valueOf(s)把字符串s解析成Integer对象类型，
            返回的integer 可以调用对象中的方法。
            */
            int first=Integer.valueOf(s.substring(i,i+1));
            //取出当前元素并转换为整型--一位数
            int second=Integer.valueOf(s.substring(i-1,i+1));
            //取出当前元素及其之前元素并转换为整型--两位数
            if(first>=1&&first<=9) dp[i]+=dp[i-1];
            //符合要求区间，可直接加到之前编码队列
            if(second>=10&&second<=26) dp[i]+=i>1?dp[i-2]:1;
        }
        return dp[l-1];
    }
}
```
