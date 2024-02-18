---
title: Binary Search Tree Insert & Remove
description: INCOMPLETE
layout: nested
---

# Binary Search Tree Insert & Remove

## Insert

 ```python
 def insert(root: Node, val: int) -> None:
    if not root:
        return Node(val)

    if val > root.val:
        root.right = insert(root.right, val)
    if val < root.val:
        root.left = insert(root.left, val)
 ```

 Time complexity: O(h) where h is the height of the tree, O(logN) if balanced.

## Remove

Requires method to find minimum value node:
 ```python
def min_value_node(root: Node) -> Node:
    curr = root
    while curr and curr.left:
        curr = curr.left
    return curr
 ```

There are two cases to consider:

 - 0 or 1 children
 - 2 children

Case 1:


 ```python
def remove(root: Node, val: int) -> None:
    if not root:
        return None

    if val > root.val:
        root.right = remove(root.right, val)
    elif val < root.val:
        root.left = remove(root.left, val)
    else: # Found value
        if not root.left:
            return root.right
        elif not right.right:
            return root.left
        else:
            min_node = min_value_node(root.right)
            root.val = min_node.val
            root.right = remove(root.right, min_node.val)

    return root
 ```

Time complexity O(logN)