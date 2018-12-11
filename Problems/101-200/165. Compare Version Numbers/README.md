# 165. Compare Version Numbers
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## python solution
```python
class Solution(object):
    def compareVersion(self, version1, version2):
        """
        :type version1: str
        :type version2: str
        :rtype: int
        """
        """
        revision--调整
        思路整理:
        1)num1 num2用于存储'.'之间的数值
        2)当遍历version1, version2时，同时遇到'.'或二者之一已经遍历结束同时
        另一方此时为'.' 则比较num1,num2  比较结束后记得将二者清零
        Explanation
        1)we use num1,num2 to rapresent the number between '.'
        2)while traversing version1, version2,
        when version1[i]=='.' and version2[j]=='.' 
        or version1[i]=='.' and j==l2
        or version2[j]=='.' and i==l1
        we compare num1 and num2,after comparasion,remember to set num1
        and num2 to zero
        """
        if not version1 or not version2:return 0
        i,j=0,0
        l1,l2=len(version1),len(version2)
        num1,num2=0,0
        while i<l1 or j<l2:
            if  i<l1 and  j<l2 and version1[i]=='.' and version2[j]=='.':
                if num1>num2:return 1
                if num1<num2:return -1
                num1,num2=0,0
                i+=1
                j+=1
                continue
            elif j==l2:
                if version1[i]!='.':num1=num1*10+ord(version1[i])-ord('0')
                elif version1[i]=='.':
                    if num1>num2:return 1
                    if num1<num2:return -1
                    num1,num2=0,0
                i+=1
            elif i==l1: 
                if version2[j]!='.':
                    num2=num2*10+ord(version2[j])-ord('0')
                elif version2[j]=='.':
                    if num1>num2:return 1
                    if num1<num2:return -1
                    num1,num2=0,0
                j+=1
            elif version1[i]!='.' and version2[j]=='.':
                num1=num1*10+ord(version1[i])-ord('0')
                i+=1
                continue
            elif version1[i]=='.' and version2[j]!='.':
                num2=num2*10+ord(version2[j])-ord('0')
                j+=1
                continue
            elif version1[i]!='.' and version2[j]!='.':
                num1=num1*10+ord(version1[i])-ord('0')
                num2=num2*10+ord(version2[j])-ord('0')
                i+=1
                j+=1 
        if num1==num2:return 0
        if num1>num2:return 1
        if num1<num2:return -1
        if l1>l2 and num1>0:return 1
        if l1<l2 and num2>0:return -1
        return 0
```

## python3 solution
```python3
class Solution:
    def compareVersion(self, version1, version2):
        """
        :type version1: str
        :type version2: str
        :rtype: int
        """
        l1,l2=len(version1),len(version2)
        i,j=0,0
        while i<l1 or j<l2:
            num1,num2=0,0
            while i<l1 and version1[i]!='.':
                num1=num1*10+ord(version1[i])-ord('0')
                i+=1
            while j<l2 and version2[j]!='.':
                num2=num2*10+ord(version2[j])-ord('0')
                j+=1
            if num1>num2:return 1
            elif num1<num2:return -1
            else:
                i+=1
                j+=1
        return 0
```

## java solution
```java
/*
 String address="上海.上海市.闵行区.吴中路";
 String[] splitAddress=address.split("\\.");
 System.out.println(splitAddress[0]+splitAddress[1]+splitAddress[2]+splitAddress[3]);
 Output:上海上海市闵行区吴中路
*/
public class Solution {
    public int compareVersion(String version1, String version2) {
       String[] v1=version1.split("\\.");
       String[] v2=version2.split("\\.");
       int l1=v1.length,l2=v2.length;
       int Max=Math.max(l1,l2);
       for(int i=0;i<Max;i++)
       {
           //static int parseInt(String s)表示将字符串转化为整数
           int num1=i<l1?Integer.parseInt(v1[i]):0;
           int num2=i<l2?Integer.parseInt(v2[i]):0;
           if (num1>num2)return 1;
           else if (num1<num2)return -1;
       }
       return 0;
    }
}
```
