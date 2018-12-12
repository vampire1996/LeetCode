# 142. Linked List Cycle II
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/142.%20Linked%20List%20Cycle%20II/problem.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/142.%20Linked%20List%20Cycle%20II/example.png"/>
<img src="https://github.com/vampire1996/LeetCode/blob/master/Problems/101-200/142.%20Linked%20List%20Cycle%20II/followup.png"/>

## python solution
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def detectCycle(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        """
        思路整理:
        利用字典(hashmap) 存储链表的节点，如果node在dict中未出现,则继续后移node指针
        如果已出现，这说明有环路,返回该node即可(第一次遇到的即为环路的首元素)
        Explanation
        use dictionary to store the nodes in linked list,if current node is not
        in dict,move the pointer to next node
        if it's in the dict alraedy,just return the current node
        (the first node which is in the dict alraedy is the 1st node in the cycle)
        """
        if not head:return None
        node=head
        dict1={}
        while node:
            if dict1.get(node,None)==None:
                #get()返回指定键的值，如果值不在字典中返回默认值(此处为None)
                dict2={node:node.val}
                dict1.update(dict2)#把字典dict2的键/值对更新到dict1里
            else: return node
            node=node.next
        return None
```
