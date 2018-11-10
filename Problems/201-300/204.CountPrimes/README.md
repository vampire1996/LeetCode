# 204. Count Primes

<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/201-300/204.CountPrimes/problem.png "/>



## c solution

```c
//方案1超时了
 /*   int countPrimes(int n) {
    if(n==1||n==0||n==2) return 0;  
    int cnt=1;
    for(int i=3;i<n;i++)
    {
        for(int j=2;j<i;j++)
        {
            if(i%j==0) break;
            if(j==i-1)  cnt++;
        }      
    }
    return cnt;
}*/
//方案2
 int countPrimes(int n) {
        if(n<3) return 0;
        if(n==3) return 1;
        int cnt=n-2;//去掉其中的素数，这里已经去掉了 2和3
        bool *prime=malloc(sizeof(bool)*n+1); //非素数标志位
        int sq=sqrt(n);
        for(int i=0;i<n;i++)
        {
         prime[i]=true;
        }
        for(int i=2;i<=sq;i++)
        {
           if(prime[i])
           {
               for(int j=i*i;j<n;j+=i)//遍历所有非素数 将其标志位置为false 并在cnt中减1
               {
                   if(prime[j])
                  {
                       prime[j]=false;
                       cnt--;
                   }
               }
           }
        }
       free(prime);
       return cnt;
 }

```
