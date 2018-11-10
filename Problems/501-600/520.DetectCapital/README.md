# 520. Detect Capital
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/501-600/520.DetectCapital/problem.png"/>

## c solution
```c
bool detectCapitalUse(char* word) {
    int n=strlen(word);
    if(n==1)  return true;
    int i=1;
    if(word[0]>='a'&&word[0]<='z')
    {
        while(word[i]) if(!(word[i]>='a'&&word[i++]<='z'))  return false;
    }
    else
    {
        if(word[1]>='a'&&word[1]<='z')
        {
             i=2;
             while(word[i]) if(!(word[i]>='a'&&word[i++]<='z'))  return false; 
        }
        else
        {
             i=2;
             while(word[i])  if(!(word[i]>='A'&&word[i++]<='Z'))  return false;
        }
    }
    return true;
}
```
