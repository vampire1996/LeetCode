# 557. Reverse Words in a String III
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/501-600/557.ReverseWordsInAString%20III/problem.png"/>

## c solution
```c
//一种数据交换的方法
/*void swap(int &a,int &b)
{
    a=a^b;
    b=b^a;
    a=a^b;
}

a1=a^b
 
b=b^a1=b^a^b=a
//此时a1=a^b  b=a
a=a1^b=a^b^a=b
*/
char* reverseWords(char* s) {
    int n=strlen(s);
    int k=0,m=0;
    bool spaceFlag=false;
    char *returnString=malloc(sizeof(char)*n+1);
    for(int i=0;i<=n;i++)
    {
        if(!spaceFlag)
        {
            if(s[i]!=' ') 
            {
                spaceFlag=true;
                k=i;
            }
            returnString[i]=s[i];
        }
        else
        {
            if(s[i]==' ') 
           {
           m=i;
           for(int j=k;j<i;j++)
           {
               returnString[j]=s[--m];
           }
           returnString[i]=s[i];
           k=i+1;
           }
           else if(s[i]==NULL)
           {
                m=i;
                for(int j=k;j<i;j++)
               {
               returnString[j]=s[--m];
               }
               returnString[i]=s[i];
           }
        }
    }
    return returnString;
}
```
