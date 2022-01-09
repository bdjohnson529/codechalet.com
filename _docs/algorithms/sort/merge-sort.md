---
title: "Merge Sort"
layout: blog
order: 1
topic: Algorithms
topic_path: /docs/algorithms/index.html
---
Merge sort solves the sorting problem through recursion. The algorithm recursively splits the unsorted array into two halves, until the array has a length of one. The sorted halves are recombined by iterating through both arrays, and selecting the smaller value from each array until both halves have been combined.

```python
def merge_sort(input_array: list) -> list:
    """Sorts the input array in ascending order.
    """
    if len(input_array) > 1:
        # divide
        mid = len(input_array) // 2

        left = input_array[:mid]
        right = input_array[mid:]

        # conquer
        left = merge_sort(left)
        right = merge_sort(right)

        # combine
        output = merge(left, right)

        return output

    else:
        return input_array


def merge(a: list, b: list) -> list:
    """Merges two sorted arrays.
    """
    i = j = 0
    output = []

    while i < len(a) and j < len(b):
        if(a[i] < b[j]):
            output.append(a[i])
            i += 1
        else:
            output.append(b[j])
            j += 1

    while i < len(a):
        output.append(a[i])
        i += 1

    while j < len(b):
        output.append(b[j])
        j += 1

    return output
```

## Complexity
The merge sort algorithm can be divided into three steps: divide, conquer and combine. We will calculate the worst-case time complexity.

* The divide step splits the input array into two subarrays. Finding the middle of a list takes a constant time, and copying the list into two lists also takes a constant time. The time complexity of this step is  list is $$ O(1) $$
* The conquer step recursively calls the `merge_sort()` function on the two subarrays. Let's define $$ T(n) $$ the time it takes to make `n` recursive calls. The total time it takes to perform all recursions on both subarrays is $$ 2T(n/2) $$.
* The combine step merges two sorted lists. Conceptually this is the same as combining two sorted piles of cards. Draw the top two cards of each pile, select the smaller card, and repeat. In the worst case, you will need to draw all the cards from both stacks. The time complexity of the merge is $$ O(n) $$.

The total time complexity of the merge sort algorithm is

$$
T(n) = O(1) + 2T(n/2) + O(n)
$$

Neglecting the constant, we can simplify the time complexity

$$
T(n) = 2T(n/2) + O(n)
$$