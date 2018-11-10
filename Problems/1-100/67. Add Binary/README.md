# 67. Add Binary
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
#define tonum(c) (c - '0')
#define tochar(i) (i + '0')

char* addBinary(char* a, char* b) {
    int m = strlen(a), n = strlen(b);
    int len = (m > n ? m : n) + 1; // strlen(c)
    char* c = malloc(sizeof(char) * len + 1); // with ending null
    memset(c, '0', len+1);
    //memset()函数原型是extern void *memset(void *buffer, int c, int count)        buffer：为指针或是数组,
    //c：是赋给buffer的值,
    // count：是buffer的长度.
    c[len] = 0;
    int carry = 0;
    for (int i = 1; i <= len; i++) {
         c[len-i] = tochar((i <= m ? tonum(a[m-i]) : 0) ^ (i <= n ? tonum(b[n-i]) : 0) ^ carry);//^表示异或
         carry = ((i <= m ? tonum(a[m-i]) : 0) + (i <= n ? tonum(b[n-i]) : 0) + carry) >> 1;
    }
    return c[0] == '0' ? c+1 : c;
}
```
