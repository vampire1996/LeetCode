# 415. Add Strings
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/401-500/415.AddStrings/problem.png "/>

## c solution
```c
/*更简洁的一种方法
#define pointAt(a,b,c) (a+b-1-c)
#define getDigAt(a,b,c) (((c)<(b))?(*((a)+(b)-1-(c))-'0'):0)
char* addStrings(char* num1, char* num2) {
    int len1 = strlen(num1);
    int len2 = strlen(num2);
    char* res = malloc(5101*sizeof(char));
    *(res+5100) = 0;
    int i=0;
    int adding = 0;
    int tmp;
    while(i<len1 || i<len2){
        tmp = getDigAt(num1, len1, i) + getDigAt(num2, len2, i) + adding;
        adding = tmp/10;
        *pointAt(res, 5100, i) = tmp%10 + '0';
        i++;
    }
    if(adding!=0){
        *pointAt(res, 5100, i)=adding + '0';
        return pointAt(res, 5100, i);
    }else{
        return pointAt(res, 5100, i+1);
    }
}
*/
char* addStrings(char* num1, char* num2) {
    if(num1[0]=='0'&&num2[0]=='0') return "0";
   int len1=strlen(num1),len2=strlen(num2);
   int i=len1-1,j=len2-1;
   int carry=0;
   int n=len1>len2?len1+1:len2+1;;
   char *sum=malloc(sizeof(char)*n+1);
   memset(sum,'0',sizeof(char)*n);//必须有这句
    sum[n]=NULL;//必须把字符串的最后一位置为空 否则会出现乱码
   int l=n-1;
    while(i>=0||j>=0)
    {
        if(i>=0&&j>=0)
        {
             if(num1[i]+num2[j]+carry-2*'0'<10)
           {
            sum[l]=num1[i]+num2[j]-'0'+carry;
            carry=0;
           }
            else 
           {
            sum[l]=num1[i]+num2[j]-'0'-10+carry;
            carry=1;
           }
           i--;
           j--;
           l--;
        }
        else if(i>=0&&j<0)
        {
            if(num1[i]=='9'&&carry==1)
            {
             sum[l]='0';
             carry=1;
             i--;
             l--;
            }
            else
            {
             sum[l]=num1[i]+carry;
             carry=0;
             i--;
             l--;
            }
        }
        else if(i<0&&j>=0)
        {
            
            if(num2[j]=='9'&&carry==1)
            {
             sum[l]='0';
             carry=1;
             j--;
             l--;
            }
            else
            {
             sum[l]=num2[j]+carry;
             carry=0;
             j--;
             l--;
            }
            
        }
    }
    if(carry==1) sum[l]='1';
    if(sum[0]!='0') return sum;
    else
    {
       sum=++sum;
    }
   return sum;
}
```
