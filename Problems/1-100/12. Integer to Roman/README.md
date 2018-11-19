# 12. Integer to Roman
<img src="https://github.com/vampire1996/-leetcode/blob/master/Problems/1-100/1.TwoSum/problem.png "/>

## c solution
```c
char* intToRoman(int num) {
    char *s=(char*)malloc(sizeof(char)*20);

    char *a[13]={"M","CM","D","CD","C","XC","L","XL","X","IX","V","IV","I"};
    int value[]={1000,900,500,400,100,90,50,40,10,9,5,4,1};
    int j=0,k=0;
    for(int i=0;num>0;i++)
    {
        while(num>=value[i])
        {
            k=0;
            while(a[i][k])
            {
                s[j++]=a[i][k++];
            }
            num-=value[i];
        }
    }
    s[j]=NULL;
    return s;
}
```
## pyhton solution
```python
class Solution:
    def intToRoman(self, num):
        """
        :type num: int
        :rtype: str
        """
        s=""
        val=[1000,500,100,50,10,5,1]
        exception9={500:"CM",100:"CM",50:"XC",10:"XC",5:"IX",1:"IX"}
        exception4={500:"CD",100:"CD",50:"XL",10:"XL",5:"IV",1:"IV"}
        exceptnum9={500:900,100:900,50:90,10:90,5:9,1:9}
        exceptnum4={500:400,100:400,50:40,10:40,5:4,1:4}
        sym="MDCLXVI"
        i=0
        temp=100
        for i in range(7):
           if num>=val[i]:
               break
           if i%2==0 and i!=0:
               temp=int(temp/10)   
        firstBit=False        
        while i<7: 
         a=int(num/temp)
         if a!=9 and a!=4:
          j=0
          n=int(num/val[i])
          if n:  
           while j<n:
             s+=sym[i]
             j+=1
          if (i)%2==0 and i!=0:
            temp=int(temp/10)  
          num=num%val[i]
          i+=1
          firstBit=True
         else:
          if a==9:
            s+=exception9[val[i]]
            num-=exceptnum9[val[i]] 
          else:
            s+=exception4[val[i]]
            num-=exceptnum4[val[i]] 
          if firstBit==False and a==4 :
            i+=1 
            firstBit=True
          else :
            firstBit=True
            i+=2
          temp=int(temp/10)
         if temp==0:
                break  
         
        
        return s
```
