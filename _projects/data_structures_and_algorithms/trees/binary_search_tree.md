---
title: Binary Search Tree
description: Lorem ipsum dolor sit amet
layout: nested
---

# Binary Search Tree

Binary search trees are binary trees with an extra constraint: For all nodes, each node in it's left subtree must have a value less than its own value and vice-versa

Searching is easily implemented with recursion

 ```python
def search(root: Node, target: int) -> bool:
    if not root:
        return False

    if target > root.val:
        return search(root.right, val)
    elif target < root.val:
        return search(root.left, val)
    else:
        return True
 ```

The time complexity is O(logN) if the tree is balanced, where N is the number of nodes within (i.e. size of) the tree, but is more generally O(h) where h is the height of the tree.

The main advantage of binary search over a tree over binary search over an array is that adding values to the data structure is O(logN) compared to O(N).


