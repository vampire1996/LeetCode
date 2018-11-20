# 17. Letter Combinations of a Phone Number
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## python solution
```python
class Solution:
    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """
        mapper=["0","1","abc","def","ghi", "jkl","mno","pqrs","tuv","wxyz"]
        
        res=[]
        if len(digits)==0:
            return res
        res.append("")
        for digit in digits:
            tmp=list()
            chars=mapper[int(digit)]
            for r in res:
                for char in chars:
                    tmp.append(r+char)
            res=tmp
        return res
```

## python3 solution
```python3
class Solution:
    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """
        if not digits:
            return []
        dic={'2':"abc",'3':"def",'4':"ghi",'5':"jkl",'6':"mno",'7':"pqrs",'8':"tuv",'9':"wxyz"}
        l={'2':3,'3':3,'4':3,'5':3,'6':3,'7':4,'8':3,'9':4}
        num=len(digits)
        res=[]
        i=0
        k=0
        j=0
        for k in range(l[digits[i]]):
             res.append(dic[digits[i]][k]) 
        curlen=l[digits[i]]      
        for i in range(1,num):
            a=[]
            a+=res
            j=0
            for k in range(l[digits[i]]):
                for m in range(curlen): 
                    res[j]+=dic[digits[i]][k]
                    j+=1  
                if k!=l[digits[i]]-1:
                   res+=a   
            curlen*=l[digits[i]]
        return res  
```
