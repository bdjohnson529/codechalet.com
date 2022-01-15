---
title: "Linked Lists"
layout: blog
order: 0
topic: Algorithms
topic_path: /docs/algorithms/index.html
---
A dynamic set is a set whose elements are subject to change. Dynamic sets are ubiquitous in programming - each time you append elements to an array, you are adding elements to a dynamic set. In fact, the `array` object in Python is a dynamic array which automatically resizes itself in memory as new elements are added.

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

Now we can implement a queue with the two operations we specified above. Notice that the two methods of the `Queue` class, `enqueue` and `dequeue`, each have a runtime of $$ O(n) $$. The methods are performing a constant amount of work which does not depend on the length of the queue.

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

The final method we will build is the `search` method. The search we will implement is a simple iterative search, where we iterate over every element of the linked list. This search has a runtime of $$ O(n) $$, since it iterates over all the elements of the array.

```python
  def search(self, query):
    x = self.head

    while(x != None) and (x.value != query):
      x = x.next

    if(x != None):
      print(x.value)
    else:
      print("Not found")
```