# 155. Min Stack
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/155.%20Min%20Stack/problem.png"/>

## python solution
```python
"""
思路整理:
1)用二维数组记录数据 每一组数据分别记录进栈时的数据 和进栈后所有数据的最小值
2)getmin 只需取出最后一次进栈后所有数据的最小值self.res[-1][1]即可
explanation
1)we use a 2D matrix to store datas for each "push" operation
which include the current data and the minimum data of all data in the stack
2)so we can easily get the smallest data by taking self.res[-1][1] as our return data
"""
class MinStack(object):
    def __init__(self):
        """
        initialize your data structure here.
        """
        self.res=[]
        

    def push(self, x):
        """
        :type x: int
        :rtype: void
        """
        self.curMin=self.getMin()
        if x<self.curMin or self.curMin==None:self.curMin=x
        self.res.append([x,self.curMin])

    def pop(self):
        """
        :rtype: void
        """
        self.res.pop()

    def top(self):
        """
        :rtype: int
        """
        return self.res[-1][0]

    def getMin(self):
        """
        :rtype: int
        """
        if not self.res:return None
        return self.res[-1][1]

# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(x)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```

## java solution
```java
public class MinStack {
    int min=Integer.MAX_VALUE;
    //必须是Integer 不能是 int
    Stack<Integer> stack;

    public MinStack(){
        stack=new Stack<>();
    }
    //当x<=min时 min应变为x 此时将之前的min入栈 
    //当pop时若弹出的元素为最小值 则将当前的min置为之前入栈的x未入栈时的最小值
    public void push(int x) {
        //这里必须是<= 而不能是<
        //因为弹出时满足stack.pop()==min 的条件为x<=min
        if(x<=min){
            stack.push(min);
            min=x;
        }
        stack.push(x); 
    }

    public void pop() {
        if(stack.pop()==min)min=stack.pop();
    }

    public int top() {
       return stack.peek();
    }

    public int getMin() {
        return min;
    }
}
/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```
