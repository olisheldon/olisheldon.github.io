---
title: Depth-First Search
description: Lorem ipsum dolor sit amet
layout: nested
---

# Depth-First Search

Uses recursion.

 ```python
 def inOrder(root: Node) -> None:
    if not root:
        return
    
    inOrder(root.left)
    print(root.val)
    inOrder(root.right)
 ```
 ```python
 def preOrder(root: Node) -> None:
    if not root:
        return
    
    print(root.val)
    inOrder(root.left)
    inOrder(root.right)
 ```
 ```python
 def postOrder(root: Node) -> None:
    if not root:
        return
    
    inOrder(root.left)
    inOrder(root.right)
    print(root.val)
 ```