---
title: Backtracking
description: INCOMPLETE
layout: nested
---

# Backtracking

Question: Does a path exist from the root of a tree to a leaf node such that no nodes on the path have a value of zero.

```python
def can_reach_leaf(root: Node) -> None:
    if not root or root.val == 0:
        return False

    if not root.left and not root.right: #if leaf node
        return True

    if can_reach_leaf(root.left):
        return True
    if can_reach_leaf(root.right):
        return True
    
    return False
```

We can also print the path to the leaf node:

```python
def leaf_path(root: Node, path: list[int]) -> None:
    if not root or root.val == 0:
        return False
    path.append(root.val)

    if not root.left and not root.right: #if leaf node
        return True

    if can_reach_leaf(root.left, path):
        return True
    if can_reach_leaf(root.right, path):
        return True

    path.pop() # could not go left or right from root to reach leaf, so pop this value
    return False
```

Time complexity: O(N)