# 686. Repeated String Match
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
//方案1
/*int repeatedStringMatch(char* A, char* B) {
    int lenA=strlen(A),lenB=strlen(B);
    int times=0;
    int i=0,j=0;
    int k=0;
    while(j<lenB)
     {
        if(A[i]==B[j])
        {
            i++;
            j++;
        }
         else 
        {
            times=0;
            j=0;
            i=++k;
        }
        if(j==lenB) break;
        if(i==lenA)
        {
            if(A[i-1]==B[j-1])
            {
               times++;
               i=0;
            }
            else {return -1;}
        }
    }

    return times+1;
}*/
int repeatedStringMatch(char* A, char* B) {
    int i;
    int LenA = strlen(A);
    int LenB = strlen(B);
    char *Pos;
    
    char* TmpStr = malloc(3 * 10000*sizeof(char));
    *TmpStr = '\0';
    
    int MaxRepeat = LenB / LenA + 2;
    for(i = 1; i <= MaxRepeat; i++){
        TmpStr = strcat(TmpStr, A);
    }
    
    Pos = strstr(TmpStr, B);//返回值：若B是TmpStr的子串，则返回B在TmpStr的首次出现的地址；如果B不是TmpStr的子串，则返回NULL。
    if(Pos == NULL) return -1;
    return  MaxRepeat - (TmpStr + MaxRepeat * LenA - Pos - LenB) / LenA;//TmpStr为TmpStr首地址 加上理论上最长的字符串A的扩展 减去B在TmpStr的首次出现的地址 再减去B的长度 则为没有用的长度 除以lenA则为没有用到的A的重复的次数
}
```
