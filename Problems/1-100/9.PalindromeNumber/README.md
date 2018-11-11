# 9. Palindrome Number
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/9.PalindromeNumber/problem.png "/>

## c solution
```c
bool isPalindrome(int x) {
    if(x<0) return false;
    if(x<10) return true;
    int reverseX=0;
    int temp=x;
    while(temp!=0)
    {
       reverseX*=10;
       reverseX+=temp%10;
       temp/=10;
    }
    while(x!=0)
    {
        if(reverseX%10!=x%10) return false;
        reverseX/=10;
        x/=10;
    }
    return true;
}
```
