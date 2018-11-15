# 49. Group Anagrams
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## python solution
```python
class Solution:
    def groupAnagrams(self, strs):
        """
        :type strs: List[str]
        :rtype: List[List[str]]
        
        
        #此方法超时了 
        def isAnagram(str1,str2):
          l1=len(str1)
          l2=len(str2)
          if l1!=l2:
            return False
          A=[0  for i in range(26)]
          for i in range(l1):
             #ord(s) 将字符转换为ASCII码
             A[ord(str1[i])-ord('a')]+=1
             A[ord(str2[i])-ord('a')]-=1
          for i in range(26):
             if A[i]!=0:
               return False
          return True  
 
        res=[]
        s=[]
        l=len(strs)
        flag=[0  for i in range(l)]
        for j in range(l):
          s=[]
          if flag[j]!=1 : 
              s.append(strs[j])
              for i in range(j+1,l):
               if flag[i]!=1 :  
                 if isAnagram(strs[j],strs[i]):
                     s.append(strs[i])     
                     flag[i]=1
              res.append(s)
            
        return res        
        """
        dict_ = {}
        res = []
        for i in range(len(strs)):
            mid = str(sorted(strs[i]))
            #str() 函数将对象转化为适于人阅读的形式。
            #sorted() 小到大排序
            if mid in dict_.keys():#返回字典所有的键 如果已经存在 则加入其对应的键值之后
                dict_[mid].append(strs[i])
            else:
                dict_[mid] = []#若不存在 则新建其键值
                dict_[mid].append(strs[i])
        for item in dict_.keys():
            res.append(dict_[item])
        return res
```
