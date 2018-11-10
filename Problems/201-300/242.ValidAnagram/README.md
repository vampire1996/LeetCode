# 242. Valid Anagram
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/201-300/258.AddDigits/problem.png"/>

## c solution
```c
bool isAnagram(char* s, char* t) {
    int c[256];
    for (int i = 0; i < 256; i++) { c[i] = 0; }
    while (*s != '\0') { c[*s++]++; }
    while (*t != '\0') { c[*t++]--; }
    for (int i = 0; i < 256; i++) {
        if (c[i] != 0) {
            return false;
        }
    }
    return true;
}
```
