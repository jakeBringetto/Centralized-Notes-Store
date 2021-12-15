---
description: >-
  Given a binary tree, find the lowest common ancestor (LCA) of two given nodes
  in the tree.
---

# Lowest Common Ancestor of a Binary Tree

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        if not root or not p or not q:
            return None
        lowest = None
        def dfs(root):
            nonlocal lowest
            if not root:
                return False
            left = dfs(root.left)
            right = dfs(root.right)
            if root.val == p.val or root.val == q.val:
                if right or left:
                    lowest = root
                    return False
                else:
                    return True
            if left and right:
                lowest = root
                return True
            return left or right
        dfs(root)
        return lowest
```
