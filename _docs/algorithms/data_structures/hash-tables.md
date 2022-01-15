---
title: "Hash Tables"
layout: blog
order: 1
topic: Algorithms
topic_path: /docs/algorithms/index.html
---
A hash table reduces the search time in a dynamic set to $$ O(1) $$. Recall that in an unsorted linked list, the worst case search time is $$ O(n) $$ as the search will need to iterate through each element in the linked list. The hash table reduces the average search time by using a *hashing function*.

The hashing function maps a set of elements onto a smaller set of elements. For example, consider the the modulus operator. The operation $$ n \bmod m $$ will reduce a set of size $$ n $$ into a set of size $$ m $$. To prove this to yourself, consider that taking the modulus of any number and 10 will yield 10 distinct values.

The hash table stores a set of keys in a smaller set of slots, using the *hashing function* to map keys to slots. Since the hash table stores more elements than it has slots, the slots of the table must be capable of storing more than one element.

A direct address hash table stores linked lists in the slots of the hash table. Specifically, the slots of the hash table are nodes in a linked list. If two elements hash to the same slot, they will both be stored in the linked list which is accessible at that slot.

### Load Factor
Let's say the hash table has $$ m $$ slots, and is used to store  $$ n $$ elements. There are fewer slots than elements, so $$ m < n $$. If we define the load factor of the hash table

$$
\alpha = \frac{n}{m}
$$

The load factor is the average number of values stored in each slot.

### Implementation
First, we will need to create nodes of a linked list.
```python
class Node:
  def __init__(self, key, value):
    self.key = key
    self.value = value
    self.prev = None
    self.next = None
```

Now, let's construct a hash table with 10 slots. We will use the modulus as our hash function. Inspect the `hash` method and you will see that the keys 19, 29, and 39 hash to the same slot. We will also construct the `insert` method for the hash table. Note that since we are inserting the element at the front of the linked list, the `insert` method has an execution time of $$ O(1) $$.

```python
class HashTable:
  def __init__(self):
    self.m = 10
    self.h = [None] * self.m

  def hash(self, key):
    return key % self.m

  def insert(self, key, value):
    index = self.hash(key)

    node = Node(key, value)

    if self.h[index]:
      node.next = self.h[index]
      self.h[index].prev = node

    self.h[index] = node
```

Next, let's construct the `search` method. Since the method searches through a linked list, the runtime is dependent on the length of the linked list. Using the definition of the load factor from above, it can be shown that the runtime of search is $$ O(1 + \alpha) $$. If the load factor is constant, i.e. if the number of slots is proportional to number of elements in the table, we can neglect $$ \alpha $$ and the runtime simplifies to $$ O(1) $$.

```python
  def search(self, key):
    index = self.hash(key)

    node = self.h[index]

    if node is None:
      return -1

    while node.key is not key:
      node = node.next
      if node is None:
        return -1

    return node
```

Finally, let's construct a `delete` method. The `delete` method will search for the key, and if it is present, the key will be deleted from the hash table. The runtime of the `delete` method will be the runtime of `search` method plus a constant. If we neglect the constant and hold the load factor constant, the runtime of `delete` becomes $$ O(1) $$.

```python
  def delete(self, key):
    node = self.search(key)

    if(node == -1):
      return -1

    if node.prev and node.next:
      node.prev.next = node.next
      node.next.prev = node.prev
    elif node.prev and not node.next:
      node.prev.next = None
    elif node.next and not node.prev:
      index = self.hash(key)
      self.h[index] = node.next
      node.next.prev = None
```
