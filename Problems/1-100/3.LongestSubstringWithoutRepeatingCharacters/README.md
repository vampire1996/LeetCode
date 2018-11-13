# 3. Longest Substring Without Repeating Characters
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
int lengthOfLongestSubstring(char* s) {
    int len=strlen(s);
    if(len==0) return 0;
    if(len==1) return 1;
    if(len==2&&s[0]==s[1]) return 1;
    else if(len==2&&s[0]!=s[1]) return 2;
    int head=1,tail=0,max=1;
    int last[128];//用于存放128个ascii的上一次出现的位置
    for(int i=0;i<128;i++)
    {
        last[i]=-1;//全部初始化为哨兵
    }
    while(head<len)
    {
        last[s[tail]]=tail;
        if(last[s[head]]>=tail) tail=last[s[head]]+1;//出现同一字符 更新尾指针
        else if(max<head-tail+1) max=head-tail+1;
        last[s[head]]=head;
        head++;
    }
    return max;
}
```
