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
        mid = len(input_array) // 2

        left = input_array[:mid]
        right = input_array[mid:]

        left = merge_sort(left)
        right = merge_sort(right)

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
The merge sort algorithm can be conceptually divided into three steps: dived, conquer and combine. The divide step splits the input array in half, and has a time complexity of $$ O(1) $$ since computing the middle of an array takes a constant time. The conquer step involves solving the two subproblems, and takes time $$ 2T(n/2) $$, where $$ T(n) $$ is the time it takes to solve the problem with an array of size $$ n $$. The combine step, or the merge, iterates through each element of the sorted array once and takes $$ O(n) $$.

The total time complexity of the merge sort algorithm is

$$
O(1) + 2T(n/2) + O(n)
$$

Neglecting the constant, we can simplify the time complexity

$$
2T(n/2) + O(n)
$$