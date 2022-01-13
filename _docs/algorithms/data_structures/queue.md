---
title: "Queues"
layout: blog
order: 0
topic: Algorithms
topic_path: /docs/algorithms/index.html
---
A queue is a dynamic set which implements a first-in, first-out policy. A queue data structure is very similar to a queue at the supermarket - the first person to enter the queue, leaves the queue. Queues supports several operations:

* enqueue : insert
* dequeue : remove and return the head of the queue

A queue can be implemented as a doubly linked list. To build a linked list, we first need to build a node which has three properties : a value, the next node, and the previous node.

```python
class Node:
  def __init__(self, value):
    self.value = value
    self.next = None
    self.prev = None
```

Now we can implement a queue with the two operations we specified above.

```python
class Queue:
  def __init__(self):
    self.head = None
    self.tail = None

  def enqueue(self, value):
    node = Node(value)

    if(self.head == None):
      self.head = node
      self.tail = node
    else:
      node.prev = self.tail
      self.tail.next = node

      self.tail = node

  def dequeue(self):
    if(self.head == None):
      print("Underflow!")

    elif(self.head == self.tail):
      tmp = self.head
      self.head = None
      self.tail = None
      print(tmp.value)

    else:
      tmp = self.head
      self.head.next.prev = None
      self.head = self.head.next
      print(tmp.value)
```