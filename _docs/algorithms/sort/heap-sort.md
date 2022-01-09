---
title: "Heap Sort"
layout: blog
order: 2
topic: Algorithms
topic_path: /docs/algorithms/index.html
---
Heap sort uses the heap data structure to sort an array. A *heap* is a complete binary tree, where each node is less than or equal to its parent. The binary tree below is a heap, because each parent node is greater than or equal to both of its child nodes.

<img src="{{ site.baseurl }}/assets/img/docs/algorithms/heap.jpg" alt="Heap">

Heaps can be represented as arrays, where the position of each array element corresponds to its position in the binary tree. The array representation of the heap pictured above would be as follows:

```python
[44, 42, 35, 33, 31, 19, 27, 10, 26, 14]
```

## Heapify
The first algorithm we will build, as part of heapsort, is the heapify algorithm. Heapify converts a binary tree into a heap. Inspect the binary tree below, and you will see that node 2 (26) violates the heap property, since its value is less than the values of its children. Let's build an algorithm to float 26 down so that the binary tree becomes a heap.  

<img src="{{ site.baseurl }}/assets/img/docs/algorithms/heapify.jpg" alt="Heap">

The input array for our algorithm is 
```python
[44, 26, 35, 42, 31, 19, 27, 10, 33, 14]
```

The following is an implementation of the heapify algorithm, as described in [Introduction to Algorithms](https://en.wikipedia.org/wiki/Introduction_to_Algorithms).
```python
def heapify(binary_tree: list, parent: int) -> list:
    """Sorts the input array in ascending order.
    """
    left = 2*parent + 1
    right = 2*parent + 2

    if(left <= len(binary_tree) - 1) and (binary_tree[left] > binary_tree[parent]):
        largest = left
    else:
        largest = parent

    if(right <= len(binary_tree) - 1) and (binary_tree[right] > binary_tree[largest]):
        largest = right

    if(largest != parent):
        tmp = binary_tree[parent]
        binary_tree[parent] = binary_tree[largest]
        binary_tree[largest] = tmp

        heapify(binary_tree, largest)

    return binary_tree
```

We can calculate the worst case runtime by noticing that `heapify` will run recursively on one of the child trees. If the parent tree has $$ n $$ nodes, the left child tree will have at most $$ 2n/3 $$ elements. The worst case runtime, is therefore defined by the following recursion

$$
T(n) \leq T(2n/3) + O(1)
$$

Aside from the recursion, the computations in the heapify algorithm take constant time. The solution to the recurrrence is

$$
T(n) = O(\log n)
$$

## Heap Build
Heapify can be used to construct a heap from an unsorted array. In order for the heapify algorithm to work, the child trees both need to be heaps. So, we need to apply heapify in a bottom up manner so that the child trees are guaranteed to be heaps before heapify is run at a node. Each element of the binary tree in the set $$ A[n/2+1, n/2+2, ... n] $$ has no children, so these nodes are one-element heaps. We need to call heapify on each element set $$ A[1, 2, ... n/2] $$ in order to arrange the rest of the binary array as a heap.

```python
def build_heap(input_array: list) -> list:
    """Builds a heap from an unordered array.
    """
    i = len(input_array) // 2 - 1

    while(i >= 0):
        input_array = heapify(input_array, i)

        print(input_array)
        i = i - 1

    return input_array
```

Previously, we found that heapify has a worst-case execution time of $$ O(\log n) $$. The heap build algorithm will make $$ n/2 $$ calls to heapify, so the time complexity of heap build is

$$
T(n) = O(\frac{n}{2} \log n)
$$

A tighter bound can be constructed on heap build, and it can be shown that the worst case execution time of heap build is

$$
T(n) = O(n)
$$

## Heap Sort
Heaps can be used to generate sorted arrays. After all, we are still building a sorting algorithm! In a heap, the maximum element will be stored at the root node. The first element of the heap will become the last element of the sorted array, if the array is sorted in ascending order.

If we remove the first element of the heap, we need to replace it with another element. What if we replaced it with the last element of the heap, so that we swapped the first and last elements of the heap? The root node of the heap would violate the heap property, but both of the child trees would still be heaps. Therefore, we only need to call heapify to restore the heap!

In this manner we can reduce the size of the heap by removing the first element, call heapify to restore the heap, and rinse and repeat. Notice that this algorithm sorts in place - the values it stores in memory do not depend on the size of the heap. 

```python
def heap_sort(input_array: list) -> list:
    """Sorts an input array in ascending order.
    """
    heap = build_heap(input_array)

    i = len(heap) - 1

    while(i >= 0):
        tmp = heap[0]
        heap[0] = heap[i]
        heap[i] = tmp

        i = i - 1

        heap = heapify(heap, i, 0)

    return heap
```

The call to `build_heap` takes $$ O(n) $$ time, and each call to `heapify` takes $$ O(lg n) $$ time. We will be making $$ (n - 1) $$ calls to `heapify`, so the time complexity of `heap_sort` is as follows

$$
T(n) = O(n \log n)
$$
