# 14. Longest Common Prefix
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/14.LongestCommonPrefix/problem.png "/>

## c solution
```c
//char**的pt来说，*(pt+i)对应的是各个字符串的首地址。
//strsSize 一维字符串数 strlen(strs[0]) 第一个字符串的长度
char* longestCommonPrefix(char** strs, int strsSize) {
    if(strsSize==0)  return """";
    if(strsSize==1)  return * strs;
    if(strlen(strs[0])==0)  return """";
   int i=0; 
   int num=0; 
   char *returnArray =NULL;
   //while(num<strlen(* strs))
    while(num<strlen(strs[0]))
        while(i<strsSize)
   {
            if(num==0)
            {
                if(strs[i][num]!=strs[i+1][num])  
                  return """";
                else
                    i++;       
            }  
            else 
           {
               if(strs[i][num]!=strs[i+1][num]) 
               {
                   returnArray =(char*)malloc(sizeof(char)*num+1); //此处必须多分配1个数 N 赋值为NULL 否则submission会报错
                   for(i=0;i<num;i++)
                   {
                   returnArray[i]=strs[0][i];
                   }
                   returnArray[i]=NULL;  
                   return returnArray;
               }
             else
             {
               i++;

             }
           }           
       if(i==strsSize-1) 
       {
           num++;
           i=0;
       }
   }
    return returnArray;
}

```
