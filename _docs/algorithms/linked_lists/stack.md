---
title: "Stacks"
layout: blog
order: 3
topic: Algorithms
topic_path: /docs/algorithms/index.html
---
A stack is a linked list which implements a LIFO ordering - the last elements to be added to the stack are the first elements to be removed from it. Let's implement a stack with the following methods:

* `pop()` - return and remove the item from the top of the stack
* `push(value)` - add an item to the stack

```python
class Node:
  def __init__(self, value):
    self.value = value
    self.next = None

class Stack:
  def __init__(self):
    self.top = None
    self.tail = None

  def push(self, value):
    node = Node(value)
    node.next = top
    top = node

  def pop(self):
    if(top is None):
      return None

    item = top.value
    top = top.next
    return item
```