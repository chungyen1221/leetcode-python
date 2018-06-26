# leetcode-python
practice and share the leetcode I solved

Try to solve leetcode questions with simple way.

## 1. Two Sum
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:
```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```
### solution
```python
class Solution:
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        cmp = nums.copy()
        for i in nums:
            cmp.pop(0)
            test = [i+j for j in cmp]
            if target in test:
                index0 = nums.index(i)
                index1 = test.index(target) + index0 +1
                return [index0, index1]
                
```
---

## 26. Remove Duplicates from Sorted Array
Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

Example 1:
```
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.
```
Example 2:
```
Given nums = [0,0,1,1,1,2,2,3,3,4],

Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

It doesn't matter what values are set beyond the returned length.
```

### solution
```python
class Solution:
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums) < 2:
            return len(nums)
        i = 0
        for j in nums[i+1:]:
            if nums[i] != j:
                nums[i+1] = j
                i += 1
        return i+1
```

---

## 771. Jewels and Stones
You're given strings J representing the types of stones that are jewels, and S representing the stones you have.  Each character in S is a type of stone you have.  You want to know how many of the stones you have are also jewels.

The letters in J are guaranteed distinct, and all characters in J and S are letters. Letters are case sensitive, so "a" is considered a different type of stone from "A".

Example 1:
```
Input: J = "aA", S = "aAAbbbb"
Output: 3
```
Example 2:
```
Input: J = "z", S = "ZZ"
Output: 0
```
Note:

S and J will consist of letters and have length at most 50.
The characters in J are distinct.

### solution
```python
class Solution:
    def numJewelsInStones(self, J, S):
        """
        :type J: str
        :type S: str
        :rtype: int
        """
        money = 0
        for i in S:
            if i in J:
                money +=1
        return money
```
---
## 665. Non-decreasing Array
Given an array with n integers, your task is to check if it could become non-decreasing by modifying at most 1 element.

We define an array is non-decreasing if array[i] <= array[i + 1] holds for every i (1 <= i < n).

Example 1:
```
Input: [4,2,3]
Output: True
Explanation: You could modify the first 4 to 1 to get a non-decreasing array.
```
Example 2:
```
Input: [4,2,1]
Output: False
Explanation: You can't get a non-decreasing array by modify at most one element.
```
Note: The n belongs to [1, 10,000].

### solution
```python
class Solution:
    def checkPossibility(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        # non-decreasing means increasing or equal
        if len(nums) <= 2 :
            return True
        error = 0
        for i in range(len(nums)-1):
            if nums[i] > nums[i+1]:
                error += 1
                if i == 0:
                    nums[0] = nums[1]
                elif ((i != len(nums)-2) and (nums[i-1] <= nums[i+1])):
                    nums[i] > nums[i-1]
                else:
                    nums[i+1] = nums[i]  
        if error > 1:
            return False
        else:
            return True
```
---

## 155. Min Stack
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

push(x) -- Push element x onto stack.
pop() -- Removes the element on top of the stack.
top() -- Get the top element.
getMin() -- Retrieve the minimum element in the stack.
Example:
```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```
### solution
```python
class MinStack:

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.Q = []

    def push(self, x):
        """
        :type x: int
        :rtype: void
        """
        self.Q.append(x)

    def pop(self):
        """
        :rtype: void
        """
        if len(self.Q) == 0:
            return None
        else:
            return self.Q.pop(len(self.Q)-1)

    def top(self):
        """
        :rtype: int
        """
        if len(self.Q) == 0:
            return None
        else :
            return self.Q[(len(self.Q)-1)]        

    def getMin(self):
        """
        :rtype: int
        """
        if len(self.Q) == 0:
            return None
        else :
            return min(self.Q)          


# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(x)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```
---

## 160. Intersection of Two Linked Lists
Write a program to find the node at which the intersection of two singly linked lists begins.


For example, the following two linked lists:
```
A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3
begin to intersect at node c1.
```
Notes:

If the two linked lists have no intersection at all, return null.
The linked lists must retain their original structure after the function returns.
You may assume there are no cycles anywhere in the entire linked structure.
Your code should preferably run in O(n) time and use only O(1) memory.
### solution
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

"""
They must have same nodes after the intersection point.
L1+L2 must have same tail from the intersection point as L2 + L1, so that we can move each time
"""
class Solution(object):
    def getIntersectionNode(self, headA, headB):
        """
        :type head1, head1: ListNode
        :rtype: ListNode
        """
        pA, pB = headA, headB
        if (pA == None) or (pB == None):
            return None
        while pA and pB:
            if pA == pB:
                return pA
            pA = pA.next
            pB = pB.next
            if (pA == None) and (pB == None):
                return None
            elif pA == None:        # if pA is end, connect to headB once 
                    pA = headB
            elif pB == None:        # if pB is end, connect to headA once
                    pB = headA
        return None
```
---

## 102. Binary Tree Level Order Traversal
Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example:
```
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
```
return its level order traversal as:
```
[
  [3],
  [9,20],
  [15,7]
]
```
### hint
```
hint: should add if node.left
>>> b
[2, 3, 4]
>>> b.append(None)
>>> b
[2, 3, 4, None]

hint: unable to use list(root)
>>> a 
'i am king of the world'
>>> list(a)
['i', ' ', 'a', 'm', ' ', 'k', 'i', 'n', 'g', ' ', 'o', 'f', ' ', 't', 'h', 'e', ' ', 'w', 'o', 'r', 'l', 'd']
>>> [a]
['i am king of the world']
```

### solution
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def levelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        res = []
        if root == None:
            return res
        q = [root]
        while len(q) != 0:
            # res.append([node.val for node in q])
            tmp_res = []
            tmp_q = []
            for node in q:
                tmp_res.append(node.val)
                if node.left:
                    tmp_q.append(node.left)
                if node.right:
                    tmp_q.append(node.right)
            res.append(tmp_res)
            q = tmp_q
        return res
```
---













