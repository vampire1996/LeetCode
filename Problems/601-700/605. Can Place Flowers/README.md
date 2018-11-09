# 605. Can Place Flowers
## c solution
```c
bool canPlaceFlowers(int* flowerbed, int flowerbedSize, int n) {
    if(n==0) return true;
    if(flowerbedSize==1)
    {
        if(flowerbed[0]==0&&n==1) return true;
        else return false;
    }
    if(flowerbedSize==2)
    {
        if(flowerbed[0]==0&&n==1&&flowerbed[1]==0) return true;
        else return false;
    }
    int i=0;
    if(flowerbed[0]==0&&flowerbed[1]==0) 
    {
        i++;
        n--;
    }
    if(flowerbed[flowerbedSize-1]==0&&flowerbed[flowerbedSize-2]==0) 
    {
        flowerbedSize--;
        n--;
    }
    while(i<flowerbedSize-2)
    {
        if(flowerbed[i]==1) 
        {
            i++;
        }
        else if(flowerbed[i]==0&&flowerbed[i+1]==0&&flowerbed[i+2]==0)  
        {
            n--;
            i+=2;
        }
        else 
        {
            i++;
        }
    }
    if(n<=0) return true;
    else return false;
}
```
c++ solution
---
```cpp
class Solution {
public:
    bool canPlaceFlowers(vector<int>& flowerbed, int n) {
        for (int i = 0; i < flowerbed.size(); ++i) {
            if (!flowerbed[i] && (0 == i || !flowerbed[i - 1]) && (flowerbed.size() - 1 == i || !flowerbed[i + 1])) {
                flowerbed[i] = 1;
                --n;
            }
        }
        return n <= 0;
    }
};
```
