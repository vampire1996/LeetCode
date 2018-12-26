# 151. Reverse Words in a String
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## python solution
```python
class Solution(object):
    def reverseWords(self, s):
        """
        :type s: str
        :rtype: str
        """
        """
        思路整理:
        1)由于字符串是不可修改的 因此需要将其转换为数组
        2)将整个数组翻转l[:]=l[::-1]
        3)将每个单词翻转
        4)排除掉前缀和后缀中的空格
        5)排除掉两个单词间多余一个的空格
        Explanation
        1)because string can not be modified,we need to reverse it to a list
        2)reverse the whole list
        3)reverse each word in the list
        4)redeuce the leading or trailing spaces
        5)reduce multiple spaces between two words
        """
        def reverse_string(arr, l, r):
            '''reverse a given string'''
            while l < r:
                arr[l], arr[r] = arr[r], arr[l]
                l += 1 ; r -= 1
        if not s:return s
        l=list(s)
        l[:]=l[::-1]
        length=len(s)
        i=0
        #将每个单词翻转
        while i<length:
            if l[i]==' ':
                i+=1
                continue
            j=i+1
            while j<length and l[j]!=' ':j+=1
            reverse_string(l, i, j-1)
            i=j
        #排除掉前缀和后缀中的空格
        start,end=0,length-1
        while start<length and l[start]==' ':start+=1
        while end>=0 and l[end]==' ':end-=1
        if start==length or end<0:return ""
        #排除掉两个单词间多余一个的空格
        res=[l[start]]
        for i in range(start+1,end+1):
            if res[-1]==' ' and l[i]==' ':continue
            res.append(l[i])
        return "".join(res)
```

## java solution
```java
public class Solution {
  /*
  1)输入为"" 跳过for循环 直接输出out[0]=""
  2)输入为"a" 跳过for循环 直接输出out[0]="a"
  3)输入为"a b c" for循环结束后res="c b " res+out[0]="c b a"
  */
  public String reverseWords(String s) {
    return solution2(s);
   }
    //利用库函数
    private String solution1(String s)
    {
         String[] out=s.trim().split("\\s+");
         String res="";
         for(int i=out.length-1;i>0;i--)
         {
            res+=out[i]+" ";
         }
         return res+out[0];
    }
     private String solution2(String s)
    {
        if(s==null||s.length()==0)return "";
        char[] res=s.toCharArray();
        reverse(res,0,res.length-1);
        int start=0,end=0;
        for(int i=0;i<res.length;i++)
        {
            if(res[i]!=' ')
            {
                res[end++]=res[i];
            }
            else if(i>0&&res[i-1]!=' ')
            {
                reverse(res,start,end-1);
                res[end++]=' ';
                start=end;
            }
        }
        reverse(res,start,end-1);//s="the sky is blue" 最后一个单词之前未翻转
         //s="" 或s全为空格或s="a b c" res(0,end) 
         //s="a b c "   res(0,end-1) 
        return  new String(res,0,end>0&&res[end-1]==' '?end-1:end);
    }
    private char[] reverse(char[] s,int i,int j)
    {
        while(i<j)
        {
            char temp=s[i];
            s[i]=s[j];
            s[j]=temp;
            i++;
            j--;
        }
        return s;
    }
}
```
