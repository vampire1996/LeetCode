# 39. Combination Sum
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## python solution
```python
#使用DFS
class Solution(object):
    def combinationSum(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        
        res=[]
        l=len(candidates)
        def dfs(target,index,path):
          if target<0:  
              return 
          elif target==0:  
             res.append(path)  
             return 
          for i in range(index,l):
              #path不能用append 因为要始终保持path=[] 
              dfs(target-candidates[i],i,path+[candidates[i]])
            
        dfs(target,0,[])
        return res
```

## python3 solution
```python3
class Solution:
    def combinationSum(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        l=len(candidates)   
        i=l-1
        res=[]
        cur=0
        s=[]
        while i>=0:
            a=[]
            if candidates[i]==target:
                a.append(candidates[i])
            elif target%candidates[i]==0 and int(target/candidates[i]) and i==0:
               j=0
               n=int(target/candidates[i])
               for j in range(n):
                  a.append(candidates[i])
            elif target>candidates[i] and i>0:
                cur=target-candidates[i]
                s=self.combinationSum(candidates[:i+1],cur)     
                lenS=len(s)
                k=0
                if lenS:
                  while k in range(lenS):
                     s[k].append(candidates[i])
                     res.append(s[k])
                     k+=1
            if a:        
              res.append(a)
            i-=1
        return  res   
```
