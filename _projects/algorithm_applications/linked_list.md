---
title: Linked List
description: Finding Middle, Contain Cycle, Finding Cycle
layout: nested
---

# Linked List

## Finding Middle

Question: What is the middle value of this linked list?

```python
def middle_of_list(head: Node) -> Node:
    slow, fast = head, head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    return slow
```

Time complexity: O(n)
Memory complexity: O(1)

## Contain Cycle

Does the following linked list contain a cycle?
```python
def has_cycle(head: Node) -> bool:
    slow, fast = head, head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
    return False
```

Time complexity: O(n)
Memory complexity: O(1)

## Finding Cycle

Does the following linked list contain a cycle? If so return the beginning of the cycle, otherwise return None.
```python
def cycle_start(head: Node) -> Node | None:
    slow, fast = head, head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            break

    if not fast or not fast.next:
        return None
    
    slow2 = head
    while slow != slow2:
        slow = slow.next
        slow2 = slow2.next
    return slow
```

Time complexity: O(n)
Memory complexity: O(1)