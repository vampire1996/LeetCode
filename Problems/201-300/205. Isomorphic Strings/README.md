# 205. Isomorphic Strings
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/201-300/205.%20Isomorphic%20Strings/problem.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/201-300/205.%20Isomorphic%20Strings/example.png"/>

## c solution
```c
bool isIsomorphic(char* s, char* t) {
    char mapS[128],mapT[128];
    memset(mapS,0,128);
    memset(mapT,0,128);
    int len=strlen(s);
    for(int i=0;i<len;i++)
    {
        if (mapS[s[i]]==0 && mapT[t[i]]==0)
        {
            mapS[s[i]]=t[i];
            mapT[t[i]]=s[i];
        }
        else if(mapS[s[i]]!=t[i] || mapT[t[i]]!=s[i])
        {
            return false;
        }
    }
    return true;
}
```

## python solution
```python
class Solution(object):
    def isIsomorphic(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        #maps和mapt分别记录s和t中字符上次出现的位置
        maps=[-1 for i in range(128)]
        mapt=[-1 for i in range(128)]
        l=len(s)
        for i in range(l):
            if maps[ord(s[i])] is not mapt[ord(t[i])]:
                return False;
            maps[ord(s[i])]=i;
            mapt[ord(t[i])]=i;
        return True 
```

## python3 solution
```python3
class Solution:
    def isIsomorphic(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        mapS=['' for i in range(128)]
        mapT=['' for i in range(128)]
        l=len(s)
        for i in range(l):
            if not mapS[ord(s[i])] and not mapT[ord(t[i])]:
                mapS[ord(s[i])]=t[i]
                mapT[ord(t[i])]=s[i]
            elif mapS[ord(s[i])] is not t[i] or mapT[ord(t[i])] is not s[i]:
                return False
        return True  
```
