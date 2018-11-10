# 551. Student Attendance Record I
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/501-600/551.StudentAttendanceRecord%20I/problem.png"/>

## c solution
```c
bool checkRecord(char* s) {
    int cntA=0,cntL=0;
    while(*s)
    {
        if(*s=='A') 
        {
            cntA++;
            cntL=0;
        }
        if(*s=='L') cntL++;
        if(*s=='P') cntL=0;
        if(cntA>1||cntL>2) return false;
        s++;
    }
    return true;
}
```
