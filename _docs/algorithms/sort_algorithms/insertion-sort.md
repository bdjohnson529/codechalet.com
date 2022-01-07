---
title: "Insertion Sort"
layout: blog
order: 2
topic: Algorithms
topic_path: /docs/algorithms/index.html
---
Insertion sort iterates through the input array, and inserts each member of the input array into the proper position in the output array.

```python
def insertion_sort(input_arr):
    """Sorts the input array in ascending order.
    """
    for j in range(1, len(input_arr)):

        key = input_arr[j]

        i = j-1

        while i >= 0 and input_arr[i] > key:
            input_arr[i+1] = input_arr[i]
            i = i - 1

        input_arr[i+1] = key


    return input_arr
```

## Complexity
Notice that in the worst case, the input array will be sorted in reverse order. If we define the number of elements in the input array as $$ n $$, the algorithm will need to iterate through the array $$ n $$ times, and perform $$ n $$ swaps for each iteration.

As a back of the napkin calculation, the algorithm will be performing approximately $$ n^2 $$ computations. The time complexity is $$ n^2 $$.

$$
O(n) = n^2
$$