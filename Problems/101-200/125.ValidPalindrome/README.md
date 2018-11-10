# 125. Valid Palindrome
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
bool isPalindrome(char* s) {
    int i=0;
    int j=strlen(s)-1;
       while(i<j)
        {
           if(!((s[i]<='z'&&s[i]>='a')||(s[i]<='Z'&&s[i]>='A')||(s[i]>='0'&&s[i]<='9')))  
           {
               i++;
               continue;//跳出本次循环 防止连续有两个除数字和字母的字符
               }
            if(!((s[j]<='z'&&s[j]>='a')||(s[j]<='Z'&&s[j]>='A')||(s[j]>='0'&&s[j]<='9')))  
            {
                j--;
                continue;
            }
            if(s[i]<='z'&&s[i]>='a')  s[i]=s[i]-'a'+'A';
            if(s[j]<='z'&&s[j]>='a')  s[j]=s[j]-'a'+'A';
            if(s[i]==s[j])
            {
                i++;
                j--;
                 continue;
            }
              else
              return false;
       }
     return true; 
    /*我自己写的 可以运行处结果 但是超时了
   for(i=0;i<strlen(s);i++)
    {
      if((s[i]<='z'&&s[i]>='a')||(s[i]<='Z'&&s[i]>='A')||(s[i]>='0'&&s[i]<='9'))
      {
          s1[j++]=s[i];
      }
    }
        if(((s1[i]<='z'&&s1[i]>='a')||(s1[i]<='Z'&&s1[i]>='A'))&&((s1[j-i-1]<='z'&&s1[j-i-1]>='a')||(s1[j-i-1]<='Z'&&s1[j-i-1]>='A')))
            {
              if((s1[i]==s1[j-i-1])||(s1[i]==s1[j-i-1]+'A'-'a')||(s1[i]==s1[j-i-1]+'a'-'A'))
              continue;
              else
              return false;
            }
            else
            {
               if(s1[i]==s1[j-i-1])
              continue;
              else
              return false;
            }
        }
   return true; */
}
```
