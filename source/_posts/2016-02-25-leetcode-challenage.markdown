---
layout: post
title: "leetcode challenage"
date: 2016-02-25 11:02
comments: true
categories: 
---

###Nim Game
这是最简单的题目了，但也想了很久，只想到用递归，看了答案才知道原来一条代码可以解决。。

这个问题的关键是给出一个数字，判断是否一定能赢，而不管过程。

一开始想到递归：

``` python nim-game-iter
class Solution(object):
    def canWinNim(self, n):
        """
        :type n: int
        :rtype: bool
        """
        if n == 4:
            return False
        elif n == 1 or n == 2 or n == 3:
            return True
        else:
            return not self.canWinNim(n-1) or not self.canWinNim(n-2) or not self.canWinNim(n-3)
```
提示超时，继续尝试，增加memorization，对于已经计算过的做缓存，下次遇到直接返回。

``` python nim-game-iter-memo
class Solution(object):
    def __init__(self):
        self.memo = {}
        
    def canWinNim(self, n):
        try:
            return self.memo[n]
        except KeyError:
            self.memo[n] = self.canWinNimIter(n)
            return self.memo[n]
    def canWinNimIter(self, n):
        """
        :type n: int
        :rtype: bool
        """
        if n == 4:
            return False
        elif n == 1 or n == 2 or n == 3:
            return True
        else:
            return not self.canWinNim(n-1) or not self.canWinNim(n-2) or not self.canWinNim(n-3)
```
这次不提示超时了，提示超出最大递归深度，尼玛。。

看了别人的答案，眼泪留下来。。
``` python nim-game-superman
class Solution(object):
    
    def canWinNim(self, n):
        return n % 4 != 0
```
思考：对于4个的情况，先拿肯定是输，所以能赢的情况必然是不能被4整除的情况（一个数被4除，要么余1 2 3，要么整除）。设想一次游戏，总数除4后余1，那么你先拿一个，然后剩下总数为4的倍数，不管对方拿多少个，我只要确定我下次拿的数目跟对方上次拿的数目之和等于4即可，这样直至拿完，肯定赢。

参考：[https://www.hrwhisper.me/leetcode-nim-game/](https://www.hrwhisper.me/leetcode-nim-game/)

### Maximum Depth of Binary Tree
找出一棵二叉树的最大深度。

思路：递归，先得到左边的深度，再得到右边的深度，最后返回最大的一个即可。

```python maximum-depth-of-binary-tree
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def maxDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root:
            return 0
        else:
            left = 1 + self.maxDepth(root.left)
            right = 1 + self.maxDepth(root.right)
            return max(left, right)
```
### Invert Binary Tree

### Move Zeroes

```python move zeroes
class Solution(object):
    def moveZeroes(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        j = 0
        for i in range(len(nums)):
            if nums[i]:
                nums[i], nums[j] = nums[j], nums[i]
                j += 1
```
