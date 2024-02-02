---
title: Binary Tree
description: Insert, Remove, Search, DFS, BFS
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


## Binary Search Tree Insert & Remove

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

## Binary Search Tree

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





## Breadth-First Search

Not suited to recursion. We use a queue (FIFO) instead.

 ```python
 def bfs(root: Node) -> None:
    queue = deque()

    if root:
        queue.append(root)

    level = 0
    while len(queue) > 0:
        print(f"level {level}") # this tracking of level is unnecessary for BFS
        for i in range(len(queue)): # but it can be useful
            curr = queue.popleft()
            print(curr.val)
            if curr.left:
                queue.append(curr.left)
            if curr.right:
                queue.append(curr.right)
        
        level += 1
 ```

Set and Map data structures can be implemented using binary search trees.



## Depth-First Search

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


