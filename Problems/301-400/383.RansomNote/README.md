# 383. Ransom Note
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
//方法1 4ms
/*
bool canConstruct(char* ransomNote, char* magazine) {
    if(ransomNote[0]==NULL&&magazine[0]==NULL)  return true;
    if(ransomNote[0]==NULL&&magazine[0]!=NULL)  return true;
    if(ransomNote[0]!=NULL&&magazine[0]==NULL)  return false;
    int i=0,j=0;
    int len1=strlen(ransomNote),len2=strlen(magazine);
    char swap=NULL;
    while(i<len1)
        {
        j=0;
        while(j<len2)
        {
            if(ransomNote[i]==magazine[j])
            {
                swap=magazine[j];
                magazine[j]=magazine[len2-1];
                magazine[len2-1]=swap;
                len2--;           
                i++;
                break;
            }
            if(j==len2-1) return false;
             j++;
        }
    
        }
    return true;
    
}
*/
//方法2 4ms
//char * q = magazine;
//char *p =ransomNote; 使用这种方法赋值 使p和ransomNote相等
bool canConstruct(char* ransomNote, char* magazine) {
    int str[128]={0};
    while(*magazine)
    {
        str[*magazine]++;
        magazine++;
    }
    while(* ransomNote)
    {
        if(str[* ransomNote]==0) return false;
        str[* ransomNote]--;
        ransomNote++;
    }
    return true;
}
```
