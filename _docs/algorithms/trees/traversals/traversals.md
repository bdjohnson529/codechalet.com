---
title: "Tree Traversals"
layout: blog
order: 1
topic: Graphs
topic_path: /docs/algorithms/trees/index.html
---
An in-order traversal is graph traversal where the order of visitation is the left child, the parent node, and finally the right child. When the traversal is performed on a binary search tree, the traversal will visit the nodes in ascending order.

Let's use our [`BinarySearchTree`](binary-tree.html) class to construct a binary tree.

```python
tree = BinarySearchTree()
tree.insert(4)
tree.insert(7)
tree.insert(3)
tree.insert(9)
```

A simple in-order traversal will make use of recursion.

```python
def in_order_traversal(node, traversal=None):
  if(node != None):
    in_order_traversal(node.left)
    print(node.key)
    in_order_traversal(node.right)
```

The elements in the binary tree will be printed in ascending order - using the binary tree we created above:

```python
3, 4, 7, 9
```

## Pre-Order Traversal
A pre-order traversal is graph traversal where the order of visitation is the parent node, the left child, and finally the right child. We can construct a simple pre-order traversal using recursion.

```python
def pre_order_traversal(node):
  if(node != None):
    print(node.key)
    pre_order_traversal(node.left)
    pre_order_traversal(node.right)
```

The elements in the binary tree will be printed in ascending order - using the binary tree we created above:

```python
4, 3, 7, 9
```

## Post-Order Traversal
A post-order traversal is graph traversal where the order of visitation is the left child, the right child, and finally the parent node. We can construct a simple pre-order traversal using recursion.

```python
def post_order_traversal(node):
  if(node != None):
    pre_order_traversal(node.left)
    pre_order_traversal(node.right)
    print(node.key)
```

The elements in the binary tree will be printed in ascending order - using the binary tree we created above:

```python
3, 7, 9, 4
```