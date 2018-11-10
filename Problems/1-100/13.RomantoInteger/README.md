# 13. Roman to Integer
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/13.RomantoInteger/problem.png "/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/13.RomantoInteger/example.png "/>
## c solution
```c
bool Iflag=false;
bool Xflag=false;
bool Cflag=false;
void clearFlag()
{
    Iflag=false;
    Xflag=false;
    Cflag=false;
}
int romanToInt(char* s) {
    int sum=0;
    int i=0;
    bool Iflag=false;
    bool Xflag=false;
    bool Cflag=false;
    while(i<strlen(s))
    {
        switch (s[i++])
        {
        case 'I':
           sum+=1;
           Iflag=true;
           Xflag=false;
           Cflag=false;
           break;
        case 'V':
            if(Iflag==true)
            {
                sum+=3; 
                Iflag=false;
            } 
            else
            {
                sum+=5;  
                Xflag=false;
                Cflag=false; 
            }
             break; 
        case 'X':
           if(Iflag==true)
            {
                sum+=8; 
                Iflag=false;
            } 
            else
            {
                sum+=10;  
                Xflag=true;
                Cflag=false; 
            }
             break;
        case 'L':
              if(Xflag==true)
            {
                sum+=30; 
                Xflag=false;
            } 
            else
            {
                sum+=50;  
                Iflag=false;
                Cflag=false; 
            }
             break;
        case 'C':
            if(Xflag==true)
            {
                sum+=80; 
                Xflag=false;
            } 
            else
            {
                sum+=100;  
                Iflag=false;
                Cflag=true; 
            }
             break;
        case 'D':
             if(Cflag==true)
            {
                sum+=300; 
                Cflag=false;
            } 
            else
            {
                sum+=500;  
                Iflag=false;
                Xflag=false; 
            }
             break;
        case 'M':
             if(Cflag==true)
            {
                sum+=800; 
                Cflag=false;
            } 
            else
            {
                sum+=1000;  
                Iflag=false;
                Xflag=false; 
            }
             break;
        default: break;
        }
    }
    return sum;
}
```
