# 121. Best Time to Buy and Sell Stock
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/121.BestTimetoBuyandSellStock/problem.png "/>

## python solution
```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        """
        The logic to solve this problem is same as "max subarray problem" using Kadane's Algorithm. Since no body has mentioned this so far, I thought it's a good thing for everybody to know.
        All the straight forward solution should work, but if the interviewer twists the question slightly by giving the difference array of prices, Ex: for {1, 7, 4, 11}, if he gives {0, 6, -3, 7}, you might end up being confused.
        Here, the logic is to calculate the difference (maxCur += prices[i] - prices[i-1]) of the original array, and find a contiguous subarray giving maximum profit. If the difference falls below 0, reset it to zero.
       """
        maxCur=0
        maxSoFar=0
        l=len(prices)
        for i in range(1,l):
            maxCur+=prices[i]-prices[i-1]
            maxCur=max(0,maxCur)
            maxSoFar=max(maxCur,maxSoFar)
        return maxSoFar   
```

## python3 solution
```python3
class Solution:
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        if not prices:
            return 0
        maxPrice=prices[0]
        maxIndex=0
        minPrice=prices[0]
        minIndex=0
        profit=0
        l=len(prices)
        for i in range(l):
            if maxPrice<prices[i]:
                  maxPrice=prices[i]
                  maxIndex=i
            if minPrice>prices[i]:
                  minPrice=prices[i]
                  minIndex=i
            if  maxIndex<=minIndex:
                 maxPrice=prices[i]
                 maxIndex=i
            if   maxIndex>minIndex and maxPrice-minPrice>profit:
                profit=maxPrice-minPrice
        return profit      
```
