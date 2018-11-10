# 345. Reverse Vowels of a String
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
bool isVowel(char letter)
{
   if(letter=='a'||letter=='e'||letter=='i'||letter=='o'||letter=='u'||letter=='A'||letter=='E'||letter=='I'||letter=='O'||letter=='U')           return  true;
    else return false;
}
char* reverseVowels(char* s) { 
    int len=strlen(s);
    int i=0,j=len-1;
    char *s_v=malloc(sizeof(char)*(len+1));
    while(i<=j)
    {
        if(!isVowel(s[i])) 
        {
            s_v[i]=s[i];
            i++; 
        }
        if(!isVowel(s[j])) 
        {
            s_v[j]=s[j];         
            j--; 
            continue;
        }
        if(isVowel(s[i])&&isVowel(s[j]))
        {
           s_v[i]=s[j];
           s_v[j]=s[i];
           i++;
           j--; 
           continue;
        }

    }
    s_v[len]=NULL; 
    return  s_v;    
}
```
