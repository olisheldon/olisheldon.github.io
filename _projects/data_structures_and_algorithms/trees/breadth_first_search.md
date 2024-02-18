---
title: Depth-First Search
description: Lorem ipsum dolor sit amet
layout: nested
---

# Depth-First Search

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