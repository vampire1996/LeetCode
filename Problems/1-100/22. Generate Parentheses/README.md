# 22. Generate Parentheses
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/1-100/14.LongestCommonPrefix/problem.png "/>

## python3 solution
```python3
"""
yield 的作用就是把一个函数变成一个 generator，带有 yield 的函数不再是一个普通函数，Python 解释器会将其视为一个 generator，在 for 循环执行时,返回一个 iterable 对象
"""
class Solution:
    def generateParenthesis(self, n):
        def generate(p, left, right):
            if right >= left >= 0:
                if not right:
                    yield p
                for q in generate(p + '(', left-1, right): yield q
                for q in generate(p + ')', left, right-1): yield q
        return list(generate('', n, n))
```
