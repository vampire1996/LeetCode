# 680. Valid Palindrome II
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
//validPalindrome 有效回文
/*bool validPalindrome(char* s) {
    int len=strlen(s);
    int i=0,j=len-1;
    bool delateFlag=true;
    while(i<j)
    {
        if(s[i]==s[j]) {i++;j--;}
        else
        {
            if(j-i==1) return true;
            if(delateFlag==true){
               if(s[i+1]==s[j]||s[i]==s[j-1]) 
                   {
                      if(i<j-3)
                      {
                          if(s[i+2]==s[j-1]&&s[i+1]==s[j])
                          {
                              i+=3;
                              j-=2;
                          }
                          else if(s[i+1]==s[j-2]&&s[i]==s[j-1])
                          {
                              i+=2;
                              j-=3;
                          }
                          else
                          {
                              return false;
                          }
                        delateFlag=false;       
                      }
                      else {return true; }
                   }              
               else {return false; }   
            }
            else
            {
                
                return false;
            }  
        }
    }
    return true;
}*/
//方案2
int diff(char *s,int n)
{
    if(n<2) return -1;
    for(int i=0,j=n-1;i<j;i++,j--)
    {
        if(s[i]!=s[j]) return i;
    }
    return -1;
}
bool validPalindrome(char* s) {
   int len=strlen(s);
   int index=diff(s,len);
    if(index==-1) return true;
    else len-=2*index+1;
    return diff(s+index,len)==-1||diff(s+index+1,len)==-1;
}
```
