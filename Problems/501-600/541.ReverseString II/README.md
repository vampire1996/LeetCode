# 541. Reverse String II
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
char* reverseStr(char* s, int k) {
    if(k==1) return s;
    int len=strlen(s);
    int j=0,m=0;
    char *returnString=malloc(sizeof(char)*len+1);
    for(int i=0;i<len;i++)
    {
        if(len<=k)
        {
            returnString[i]=s[len-i-1];
        }
        else
        {
            if(i%(2*k)==0) j=i;
            if(j+k<len)
            {
                if(i%(2*k)<k)
                {
                  returnString[i]=s[j+k-1-m]; 
                  m++;
                  if(m==k) m=0;
                }
                else
                {
                    returnString[i]=s[i];
                } 
            }
            else if(j+k>=len&&i%(2*k)<k)
            {
                returnString[i]=s[len-1-m];
                 m++;
            }
            else 
            {
                returnString[i]=s[i];
            }
        }
    }
    returnString[len]=NULL; 
    return returnString;
}
//另一种方法
/*
void reverse(int start,int end,char *s)
{
    char tmp;
    while(start < end)
    {
        tmp = s[end];
        s[end--] = s[start];
        s[start++] = tmp;
    }
}

char* reverseStr(char* s, int k) 
{
    int len = strlen(s);
    if(len <= k)
    {
        reverse(0,len - 1,s);
        return s;
    }
        
    for (int i = 0; i < len; i += 2 * k) 
    { 
        if(i + 2*k <=len)// at least 2k left
        {
            reverse(i,i + k - 1,s);
        } 
        else if(len - i >= k) //more than or equal to k left
        {
            reverse(i,i + k - 1,s);
            break;
        }
        else if(len - i < k)//less than k,reverse i to len-1
        {
            reverse(i,len - 1,s);
            break;
        }
    }  
    
    return s;
    
}*/
```
