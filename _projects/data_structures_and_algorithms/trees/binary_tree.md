---
title: Binary Tree
description: Lorem ipsum dolor sit amet
layout: nested
---

# Binary Tree

 - No cycles
 - Each node can have 0, 1 or 2 children
 - A node with no parents is the root node
 - Node with no children are called leaf nodes
 
 A tree is said to be balanced if the following three conditions hold:

 - The height of the left and right tree for any node does not differ by more than 1.
 - The left subtree of that node is also balanced.
 - The right subtree of that node is also balanced.

 ```python
class Node:

    def __init__(self, val: int):
        self.left = None
        self.right = None
        self.val = val

    def set_left(self, left: 'Node') -> None:
        self.left = left

    def set_right(self, right: 'Node') -> None:
        self.right = right
 ```

