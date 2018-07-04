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
![tt](BFS-DFS.png)

### solution - BFS
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

### solution - DFS
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
        depth = 0
        self.dfs(root, depth, res)
        return res
    def dfs(self, tmp_root, tmp_depth, tmp_res):
        if tmp_root == None:
            return tmp_res
        if len(tmp_res) < tmp_depth + 1:
            tmp_res.append([])
        tmp_res[tmp_depth].append(tmp_root.val)
        self.dfs(tmp_root.left, tmp_depth+1, tmp_res)
        self.dfs(tmp_root.right, tmp_depth+1, tmp_res)
```
---

## 199. Binary Tree Right Side View
Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

Example:
```
Input: [1,2,3,null,5,null,4]
Output: [1, 3, 4]
Explanation:

   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
```

### solution - BFS
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def rightSideView(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        res = []
        if root == None:
            return res
        q = [root]
        while len(q) != 0:
            res.append(q[len(q)-1].val)
            tmp_q = []
            for node in q:
                if node.left:
                    tmp_q.append(node.left)
                if node.right:
                    tmp_q.append(node.right)
            q = tmp_q
        return res
```
---

## 20. Valid Parentheses
Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Note that an empty string is also considered valid.

Example 1:
```
Input: "()"
Output: true
```
Example 2:
```
Input: "()[]{}"
Output: true
```
Example 3:
```
Input: "(]"
Output: false
```
Example 4:
```
Input: "([)]"
Output: false
```
Example 5:
```
Input: "{[]}"
Output: true
```

### solution
```python
class Solution:
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        # use stack to solve the problem 
        # if when the left side ends, the first right side must be pair with the last left side

        # must be pair
        l_s = len(s)
        if l_s == 0:
            return True
        elif l_s % 2 != 0:
            return False
        
        stack = [] # make stack
        v_dic = {  ")":"(",   "]":"[",   "}":"{"  } # mapping
        
        if s[0] not in v_dic.values():
            return False
        
        for char in s: 
            if char in v_dic.values():
                stack.append(char)
            elif char in v_dic.keys():
                if v_dic[char] != stack.pop():
                    return False
            else: 
                return False
        if stack == []:
            return True
        else:
            return False
```
---

## 200. Number of Islands
Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example 1:
```
Input:
11110
11010
11000
00000

Output: 1
```
Example 2:
```
Input:
11000
11000
00100
00011

Output: 3
```
### solution
```python
class Solution:
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        """
        Use DFS, once it touch 1s, continue to search near part form up/down/left/right
        count of island + 1
        And then change the sysbol to anaother for avoiding next search
        """
        count = 0
        if not grid:
            return 0
        range_x = range(len(grid))     # range for x axis
        range_y = range(len(grid[0]))        # range for y axis
        #print("{},{}".format(range_x, range_y))
        for x in range_x:
            for y in range_y:
                if grid[x][y] == '1':
                    count += 1          # find an island
                    self.dfs(grid, x, y)
        return count
    
    def dfs(self, tmp_grid, tmp_x, tmp_y):
        print("{},{}".format(tmp_x, tmp_y))
        if tmp_x < 0 or tmp_x >= len(tmp_grid) or tmp_y < 0 or tmp_y >= len(tmp_grid[0]) :
            return
        if tmp_grid[tmp_x][tmp_y] != '1':
            return
        tmp_grid[tmp_x][tmp_y] = "E"            # change to anather symbol
        self.dfs(tmp_grid, tmp_x - 1, tmp_y)    # change neighborhood -x direction
        self.dfs(tmp_grid, tmp_x + 1, tmp_y)    # change neighborhood x direction
        self.dfs(tmp_grid, tmp_x, tmp_y - 1)    # change neighborhood -y direction
        self.dfs(tmp_grid, tmp_x, tmp_y + 1)    # change neighborhood y direction
 ```
 ---

## 204. Count Primes
Count the number of prime numbers less than a non-negative number, n.

Example:
```
Input: 10
Output: 4
Explanation: There are 4 prime numbers less than 10, they are 2, 3, 5, 7.
```
### solution
```python
class Solution:
    def countPrimes(self, n):
        """
        :type n: int
        :rtype: int
        """
        """
        import math as math0
        
        if n <= 2:          # no prime numbers less than 2
            return 0
        count = 1           # if n >= 3, at least has one prime number 2
        nums = [1]*n        # list form index 0 to index n-1
        nums[0], nums[1] = 0,0  # 0 and 1 is not prime number
        """
        if n <= 2:
            return 0
        res = [True] * n
        res[0] = res[1] = False
        for i in range(2, n):
            if res[i] == True:
                for j in range(2, (n-1)//i+1):
                    res[i*j] = False
        return sum(res)


```
---
## 206. Reverse Linked List
Reverse a singly linked list.

Example:
```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```
Follow up:

A linked list can be reversed either iteratively or recursively. Could you implement both?

### hint
[一圖勝千言](https://www.polarxiong.com/archives/LeetCode-206-reverse-linked-list.html)

### solution
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if head == None:
            return head
        new_head = head
        while head.next != None:
            curr = head.next 
            head.next = curr.next
            curr.next = new_head
            new_head = curr
        return new_head
```
---

## 21. Merge Two Sorted Lists
Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Example:
```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```
### solution
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        # # recursively
        if not l1:
            return l2
        if not l2:
            return l1
        if l1.val <= l2.val:
            res = l1
            res.next = self.mergeTwoLists(l1.next, l2)
            return res
        if l1.val > l2.val:
            res = l2
            res.next = self.mergeTwoLists(l1, l2.next)
            return res
```
---


## 235. Lowest Common Ancestor of a Binary Search Tree
Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes in the BST.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”
```
Given binary search tree:  root = [6,2,8,0,4,7,9,null,null,3,5]

        _______6______
       /              \
    ___2__          ___8__
   /      \        /      \
   0      _4       7       9
         /  \
         3   5
```
Example 1:
```
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
Output: 6
Explanation: The LCA of nodes 2 and 8 is 6.
```
Example 2:
```
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
Output: 2
Explanation: The LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself 
             according to the LCA definition.
```
Note:

All of the nodes' values will be unique.
p and q are different and both values will exist in the BST.
### solution
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(self, root, p, q):
        """
        :type root: TreeNode
        :type p: TreeNode
        :type q: TreeNode
        :rtype: TreeNode
        """
        while root != None:
            if root.val > p.val and root.val > q.val: 
                root = root.left
            elif root.val < p.val and root.val < q.val:
                root = root.right
            else :
                return root
```
---

## 242. Valid Anagram
Given two strings s and t , write a function to determine if t is an anagram of s.

Example 1:
```
Input: s = "anagram", t = "nagaram"
Output: true
```
Example 2:
```
Input: s = "rat", t = "car"
Output: false
```
Note:
You may assume the string contains only lowercase alphabets.

Follow up:
What if the inputs contain unicode characters? How would you adapt your solution to such case?


### solution
```python
class Solution:
    def isAnagram(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        if len(s) != len(t):
            return False
        ss = list(s)        # so that I can use pop()
        for char in t:
            if char in ss:
                ss.pop(ss.index(char))
        if len(ss) == 0:
            return True
        else:
            return False
```
---

## 48. Rotate Image
You are given an n x n 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).

Note:

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

Example 1:
```
Given input matrix = 
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

rotate the input matrix in-place such that it becomes:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
````
Example 2:
```
Given input matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
], 

rotate the input matrix in-place such that it becomes:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
```

### solution
```python
class Solution:
    def rotate(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: void Do not return anything, modify matrix in-place instead.
        """
        """
        hint:
        1. 倒對角線互換
        2. 上下互換
        """
        # diagonal change
        for i in range(len(matrix)):
            for j in range(len(matrix)-i):
                matrix[i][j], matrix[len(matrix)-1-j][len(matrix)-1-i] = matrix[len(matrix)-1-j][len(matrix)-1-i], matrix[i][j]
        # horizontal change up side down
        for i in range(len(matrix)//2):
            for j in range(len(matrix)):
                matrix[i][j], matrix[len(matrix)-1-i][j] = matrix[len(matrix)-1-i][j], matrix[i][j]
```
---

## 49. Group Anagrams
Given an array of strings, group anagrams together.

Example:
```
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```
Note:

All inputs will be in lowercase.
The order of your output does not matter.
### solution
```python
class Solution:
    def groupAnagrams(self, strs):
        """
        :type strs: List[str]
        :rtype: List[List[str]]
        """
        """
        I am going to put strs in dict value, and sorted key
        """
        ans = {}
        for s in strs:
            s_s = ''.join(sorted(s))        # make list to string since sorted generates list
            if s_s not in ans.keys():
                ans[s_s] = []
            ans[s_s].append(s)
        return list(ans.values())
                
```
---

## 5. Longest Palindromic Substring
Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

Example 1:
```
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```
Example 2:
```
Input: "cbbd"
Output: "bb"
```
### solution
```python
class Solution:
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        """
        palindrome has two conditions: 1. odd charactors 2. even charactors
        """
        res = ""
        for i in range(len(s)):
            # find center odd
            tmp_res = self.helper(s, i, i)
            if len(tmp_res) > len(res):
                res = tmp_res
            # find center even
            tmp_res = self.helper(s, i , i+1)
            if len(tmp_res) > len(res):
                res = tmp_res
        return res
    def helper(self, s, i, j):
        ss = ''
        while (i >= 0) and (j <= len(s)-1) and (s[i] == s[j]):
            ss = s[i : j+1]
            i = i - 1
            j = j + 1
        return ss
```
---

## 78. Subsets
Given a set of distinct integers, nums, return all possible subsets (the power set).

Note: The solution set must not contain duplicate subsets.

Example:
```
Input: nums = [1,2,3]
Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```
### solution
```python
"""
DFS : for example [1,2,3], dirction: each element
                           [ ]
                        /   |   \
                     [1]   [2]   [3]
                   /  |     |
            [1, 2] [1, 3] [2, 3]
              /
        [1, 2, 3]
"""
class Solution:
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        if not nums:
            return []
        res=[[]]
        self.dfs(sorted(nums), 0, [], res)
        return res
    def dfs(self, nums, depth, node, res):
        for i in range(depth, len(nums)):
            res.append(node + [nums[i]])
            self.dfs(nums, i+1, node + [nums[i]], res)
```
---

## Codility经典算法题之二十：Fish
Task description:


You are given two non-empty arrays A and B consisting of N integers. Arrays A and B represent N voracious fish in a river, ordered downstream along the flow of the river.

The fish are numbered from 0 to N − 1. If P and Q are two fish and P < Q, then fish P is initially upstream of fish Q. Initially, each fish has a unique position.

Fish number P is represented by A[P] and B[P]. Array A contains the sizes of the fish. All its elements are unique. Array B contains the directions of the fish. It contains only 0s and/or 1s, where:

0 represents a fish flowing upstream,
1 represents a fish flowing downstream.
If two fish move in opposite directions and there are no other (living) fish between them, they will eventually meet each other. Then only one fish can stay alive − the larger fish eats the smaller one. More precisely, we say that two fish P and Q meet each other when P < Q, B[P] = 1 and B[Q] = 0, and there are no living fish between them. After they meet:

If A[P] > A[Q] then P eats Q, and P will still be flowing downstream,
If A[Q] > A[P] then Q eats P, and Q will still be flowing upstream.
We assume that all the fish are flowing at the same speed. That is, fish moving in the same direction never meet. The goal is to calculate the number of fish that will stay alive.

For example, consider arrays A and B such that:

A[0] = 4 B[0] = 0 A[1] = 3 B[1] = 1 A[2] = 2 B[2] = 0 A[3] = 1 B[3] = 0 A[4] = 5 B[4] = 0
Initially all the fish are alive and all except fish number 1 are moving upstream. Fish number 1 meets fish number 2 and eats it, then it meets fish number 3 and eats it too. Finally, it meets fish number 4 and is eaten by it. The remaining two fish, number 0 and 4, never meet and therefore stay alive.

Write a function:

class Solution { public int solution(int[] A, int[] B); }

that, given two non-empty arrays A and B consisting of N integers, returns the number of fish that will stay alive.

For example, given the arrays shown above, the function should return 2, as explained above.

Assume that:

N is an integer within the range [1..100,000];
each element of array A is an integer within the range [0..1,000,000,000];
each element of array B is an integer that can have one of the following values: 0, 1;
the elements of A are all distinct.
Complexity:

expected worst-case time complexity is O(N);
expected worst-case space complexity is O(N), beyond input storage (not counting the storage required for input arguments).
Solution:

考虑到所有鱼的速度一致，那么从上游开始check，

前面的鱼如果是往上游走的话，即永远不会被吃或者吃其他鱼,

### hint:
Put all downstream swimming fishes on a stack. Any upstream swimming fish has to fight(eat) all fishes on the stack. If there is no fish on the stack, the fish survives. If the stack has some downstream fishes at the end, they also survive.



### solution
```python
# you can write to stdout for debugging purposes, e.g.
# print("this is a debug message")

def solution(A, B):
    # write your code in Python 3.6
    eating = []
    survival = 0
    for id ,size in enumerate(A):
        if B[id] == 0:
            while eating:           # fish will make line to fight
                if eating[-1] > size: # the fish is eat
                    break
                else:               # the fish kill the coming one on the stack and wait next one
                    eating.pop()
            else: 
                survival += 1       # no one to fight, survive
        else:
            eating.append(size)
    return survival + len(eating)    
```
---


## 2. Add Two Numbers
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example
```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```
### solution
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        # non-negative: the sum must be bigger than two of it
        #--- make l1 to number
        A=[]
        while l1:
            A.append(l1.val)
            l1 = l1.next
        d = 0
        numA = 0
        for i in A:
            numA = numA + int(i) * (10**d)
            d += 1
        #--- make l2 to number
        B = []
        while l2:
            B.append(l2.val)
            l2 = l2.next
        d = 0
        numB = 0
        for i in B:
            numB = numB + int(i) * (10**d)
            d += 1
        #--- sum up 
        num = numA + numB
        #--- make it link list
        curr = ListNode(0)
        ans = curr
        if num == 0:
            return ans
        while num != 0:
            curr.next = ListNode(num % 10)
            curr = curr.next
            num = num // 10
        return ans.next
```
---

## 3. Longest Substring Without Repeating Characters
Given a string, find the length of the longest substring without repeating characters.

Examples:

Given "abcabcbb", the answer is "abc", which the length is 3.

Given "bbbbb", the answer is "b", with the length of 1.

Given "pwwkew", the answer is "wke", with the length of 3. Note that the answer must be a substring, "pwke" is a subsequence and not a substring.


### solution
```python
class Solution:
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        ans = 0
        ch = []
        for i in s:
            if i not in ch:
                ch.append(i)
            else:
                tmp = len(ch)
                ch = ch[ch.index(i)+1 :]
                ch.append(i)
                if ans < tmp:
                    ans = tmp
        if len(ch) > ans:
            return len(ch)
        else: 
            return ans
```
---


## 609. Find Duplicate File in System
Given a list of directory info including directory path, and all the files with contents in this directory, you need to find out all the groups of duplicate files in the file system in terms of their paths.

A group of duplicate files consists of at least two files that have exactly the same content.

A single directory info string in the input list has the following format:

"root/d1/d2/.../dm f1.txt(f1_content) f2.txt(f2_content) ... fn.txt(fn_content)"

It means there are n files (f1.txt, f2.txt ... fn.txt with content f1_content, f2_content ... fn_content, respectively) in directory root/d1/d2/.../dm. Note that n >= 1 and m >= 0. If m = 0, it means the directory is just the root directory.

The output is a list of group of duplicate file paths. For each group, it contains all the file paths of the files that have the same content. A file path is a string that has the following format:

"directory_path/file_name.txt"

Example 1:
```
Input:
["root/a 1.txt(abcd) 2.txt(efgh)", "root/c 3.txt(abcd)", "root/c/d 4.txt(efgh)", "root 4.txt(efgh)"]
Output:  
[["root/a/2.txt","root/c/d/4.txt","root/4.txt"],["root/a/1.txt","root/c/3.txt"]]
```
Note:
No order is required for the final output.
You may assume the directory name, file name and file content only has letters and digits, and the length of file content is in the range of [1,50].
The number of files given is in the range of [1,20000].
You may assume no files or directories share the same name in the same directory.
You may assume each given directory info represents a unique directory. Directory path and file info are separated by a single blank space.
### solution
```python
class Solution:
    def findDuplicate(self, paths):
        """
        :type paths: List[str]
        :rtype: List[List[str]]
        """
        # make a dict to put content and return dict.values
        du = collections.defaultdict(list)    # du{content:[files]}
        for i in paths:
            # seperater path and file
            data = i.split(" ")
            for j in data[1:]:
                f, g, content = j.partition("(")
                file = data[0] + "/" + f
                du[content[:-1]].append(file) 
        return [value for value in du.values() if len(value) > 1]
```
---


## 496. Next Greater Element I
You are given two arrays (without duplicates) nums1 and nums2 where nums1’s elements are subset of nums2. Find all the next greater numbers for nums1's elements in the corresponding places of nums2.

The Next Greater Number of a number x in nums1 is the first greater number to its right in nums2. If it does not exist, output -1 for this number.

Example 1:
```
Input: nums1 = [4,1,2], nums2 = [1,3,4,2].
Output: [-1,3,-1]
Explanation:
    For number 4 in the first array, you cannot find the next greater number for it in the second array, so output -1.
    For number 1 in the first array, the next greater number for it in the second array is 3.
    For number 2 in the first array, there is no next greater number for it in the second array, so output -1.
```
Example 2:
```
Input: nums1 = [2,4], nums2 = [1,2,3,4].
Output: [3,-1]
Explanation:
    For number 2 in the first array, the next greater number for it in the second array is 3.
    For number 4 in the first array, there is no next greater number for it in the second array, so output -1.
```
Note:
All elements in nums1 and nums2 are unique.
The length of both nums1 and nums2 would not exceed 1000.

### solution
```python
class Solution:
    def nextGreaterElement(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: List[int]
        """
        if not nums1:
            return nums1
        ans = []
        flag = 0
        for i in nums1:
            for j in nums2[nums2.index(i) :]:
                if j > i : 
                    ans.append(j)
                    flag = 1
                    break
            if flag == 0:
                ans.append(-1)
            flag = 0
        return ans
```
---






## 

### solution
```python

```
---
